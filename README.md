# Lab12-StatsSloths

```{r}
gapminder
```


## Is there a significant difference in the life expectancy in Asia and in Europe? 

```{r}
dataA <- gapminder_unfiltered %>%
  filter(continent =="Asia")
dataA

mean(data[["lifeExp"]])
#  Asia Life Expectancy is 62.41587

dataE <- gapminder_unfiltered %>%
  filter(continent =="Europe")
dataE

mean(dataE[["lifeExp"]])
# Europe Life Expectancy is 72.72164

72.164-62.41587
# Mean difference is 9.74813
```


```{r}
perm_mean <- function(perms = 1000, values, n1)
{
  ## Variables ##
  # perms: The number of permutations 
  # values (num): 
  # n1 (int): Size of group 1
  ###############
  
  # Step 1:
  # Create vector of zeroes of length "perms" to store
  # permuted mean differnces
  means <- vector(mode = "double", length = perms)
  
  # Loop throught number of permutations
  for (i in c(1:perms))
  {
    # Step 2
    # Shuffle them using smample
    # Randomly separate vector "values" into disjoint 
    # groups of size "n1" and "length(values) - n1" respectively
    group_one <- sample(values, n1)
    group_two <- sample(values, length(values)-n1)
    
    # Step 3:
    # Compute the sample means for the two groups from
    g1mean <- mean(group_one)
    g2mean <- mean(group_two)
    
    # Step 4: 
    # Compute the difference in sample means, store the
    # value in the vector from step 1
    diff <- g1mean - g2mean
    means[i] <- diff
  }
  
  # Step 5:
  # Return new updated vector, created in step 1
  means
  
}

new_data <- gapminder_unfiltered
life_exp <- new_data %>%
  filter(continent == "Asia" | continent == "Europe")
mean_vals <- perm_mean(1000, life_exp$lifeExp, 578)
mean_data <- data_frame(mean_vals)
ggplot(data = mean_data) +
  geom_histogram(mapping = aes(x = mean_vals), binwidth = .02)+ 
   geom_vline(xintercept =9.4578, col=c("orange")) +
  ggtitle("Distribution of Means For Europe and Asia Life Expectancy")
```
## Is there a significant correlation between GDP per capita and population? 
```{r}
cor(gapminder_unfiltered$pop, gapminder_unfiltered$gdpPercap)

# Original correlation is -0.04595259
```
```{r}
perm_cor <- function(perms = 1000, x, y)
{
  ## Variables ##
  # perms: The number of permutations 
  # x: Vector 1 - for computing correlation
  # y: Vector 2 - for computing correlation
  ###############
  
  # Step 1:
  # Create vector of zeroes of length "perms" to store
  # permuted mean differnces
  corrs <- vector(mode = "double", length = perms)
  # Loop throught number of permutations
  for (i in c(1:perms))
  {
    # Step 2:
    # Randomly mix up the values in the vector "y"
    GDP_Sample <- sample(y)
    # Step 3:
    # Compute the correlation between x and the randomly mixed
    # up y-vector. Store this value in the vector from step 1.
    correlation_value <- cor(x, GDP_Sample)
    corrs[i] <- correlation_value
  }
  
  # Step 4:
  # Return new updated vector, created in step 1
  corrs
}

corr_vals <- perm_cor(1000, new_data$pop, new_data$gdpPercap)
corr_data <- data_frame(corr_vals)
ggplot(data = corr_data) +
  geom_histogram(mapping = aes(x = corr_vals), binwidth = .001)+
  ggtitle("Distribution of Correlation Values For GDP per Capita and Population?")
```
3. Conclusion 
a. Use percentiles, summary statistics (max, min), and probabilites (p-values)






