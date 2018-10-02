---
title: "Loh_Kendall_HW1"
author: "Kendall Loh"
date: "September 23, 2018"
output: html_document
keep_md: TRUE
self_contained: true
---

```{r setup, include=FALSE}
library(knitr)
library(fivethirtyeight)
library(DT)

knitr::opts_chunk$set(echo = TRUE)
opts_chunk$set(fig.path="images/",
               cache.path="cache/",
               cache=FALSE,
               echo=TRUE,
               message=FALSE,
               warning=FALSE)  
```

# Modern Data Structures Homework #1

## 2. Let's get some data

Of the datasets contained in the fivethirtyeight package, I'm most interested in the `democratic_bench` dataset, which holds poll related to the amount of money expected to be raised and actually raised by prominent Democratic politicians. FiveThirtyEight used this data as a clue as to who was considering running for president in 2016 if Hillary Clinton decided not to run. Linked [here](http://fivethirtyeight.com/features/some-democrats-who-could-step-up-if-hillary-isnt-ready-for-hillary/), the article points to Senator Sherrod Brown, of Ohio, and Senator Al Franken, of Minnesota, as potential candidates.




```{r echo=FALSE}
data (package = "fivethirtyeight")

```

In order to get a sense of what the dataset shows, I used the ?() function. The `democratic_bench` data is a data frame with 67 rows representing members of the Democratic Party, the the three following variables: `candidate`, `raised_exp`, and `raised_act`. 

```{r}
?democratic_bench
```
#Manually create a small table for your dataframe with two columns: variable name and variable description. Include a few variables in the table.

```{r}
Variable_Name <- c("US_births_1994_2003", "ahca_polls", "airline_safety")
Variable_Description <- c("Some People Are Too Superstitious To Have A Baby On Friday The 13th", "American Health Care Act Polls","Should Travelers Avoid Flying Airlines That Have Had Crashes in the Past?")
manual_table <- data.frame(Variable_Name, Variable_Description)
print(manual_table)
```

## 3. Let's show the data

Please note that for Question #3 I split it into three parts, and hid the code for each one. In 3a I use the `summary()` function to get a simple summary. In 3b I use the `datatable()` function to get an interactive table, and in 3c I call another table using the `kable()` function.

### 3a. Provide a simple summary of the data with summary() command.
```{r echo=FALSE}

summary(democratic_bench)

```

### 3b. Use the command datatable from the package `DT` to show an interactive table of your data in the document
```{r echo=FALSE}

datatable(democratic_bench)

```

### 3c. Now add another non-interactive table using the kable function in the knitr package. Choose a sensible subset of the data (or a transformation of the data) to show. Prettify the column names a bit.

I added the kable library above, and ordered the data in alphabetical order then printed the first 5 Democratic Candidates. I also changed the column headers.

```{r echo=FALSE}
new_df = data.frame(democratic_bench)
ordered_df <- new_df[order(democratic_bench$candidate),]
ordered_df <- kable(ordered_df, col.names = c('Democratic Candidate',
                                'Expected $ Raised',
                                'Actual $ Raised'))

print(ordered_df [1:7])

```

## 4. Add some LaTex formulas.
### Think of some (any) model you run on the data you chose. This does not need to be sensible - for this homework, the formatting is the objective, the content is secondary. Briefly describe the model using a Latex formula in the text.

I think the model I would use would use k Nearest Neighbors model on multiple years of presidential elections. I would look at the residuals of each election of each candidate, and then make a prediction based on the magnitude of the residual. In this case, I would be measure the $$\epsilon$$ value in the function below.

$$ y = b_0 + (b_1)x + \epsilon $$
I'm pretty sure you could do a kNN on this problem as well. The general linear classification function is:

$$score(X_ik = B_k \cdot X_i)$$


## 5. Add a plot
I added the plot and then added axis labels.


```{r}
library(ggplot2)

i <- ggplot(democratic_bench, aes(raised_exp, raised_act)) + geom_point() + xlab('Expected $ Raised') + ylab('Actual $ Raised') + ggtitle('Scatter Plot of Democratic Bench Candidates Fundraising')

print(i)
```

## 6. Add a Picture

![This is Vermin Supreme(left), a lesser-known American Presidential Candidate](https://1fkoby17rlj41m4giv3x4cvk-wpengine.netdna-ssl.com/wp-content/uploads/2015/03/SMALL-JIMMY-MAC.jpg)
Arguably better than who we have now.

## 7. Add a footnote and a block quote.

This is a test footnote[^1]


[^1]: This is my test footnote

Block quote text below:


>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque sapien velit, aliquet eget commodo nec, auctor a sapien. Nam eu neque vulputate diam rhoncus faucibus. Curabitur quis varius libero. Lorem.

Thank you!