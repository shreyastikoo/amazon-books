# amazon-books

library(tidyverse)

path="../input/amazon-top-50-bestselling-books-2009-2019/bestsellers with categories.csv"

books <- read.csv(path)
head(books)

books$Year <- as.factor(books$Year)
books$Name <- as.character(books$Name)
books$Author <- as.character(books$Author)
str(books)

price <- books %>%
          group_by(Year) %>%
          summarise(price = mean(Price))
price

ggplot(data=price, aes(Year, price))+
    geom_col(fill="hotpink4")

books %>% ggplot(aes(User.Rating))+
            geom_histogram(binwidth = 0.25, fill="hotpink3", col="white")
            
ggplot(books, aes(x=" ", y=Genre, fill=Genre)) +
  geom_bar(stat="identity", width=1) +
  coord_polar("y", start=0)
  
books %>% ggplot(aes(Reviews))+
            geom_histogram(binwidth = 2000, alpha=0.75, fill="hotpink2")
