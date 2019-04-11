# Lab12-StatsSloths

```{r}
gapminder
```


1. Two specific questions of interest and why important and interesting 
 a. Answered with the two-sample mean permutation test
 b. Other with the correlation permutation test.


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
```

```{r}
perm_cor <- function(perms = 1000, x, y)
{
  ## Variables ##
  # perms: The number of permutations 
  # x: Vector 1 - for computing correlation
  # y: Vector 2 - for computing correlation
  ###############
  x <- vector(mode = "double", length = 
  y <- vector(mode = "double", length = 
  # Step 1:
  # Create vector of zeroes of length "perms" to store
  # permuted mean differnces
  means <- vector(mode = "double", length = perms)
  # Loop throught number of permutations
  for (i in c(1:perms))
  {
    # Step 2:
    # Randomly mix up the values in the vector "y"
    GDP_Samples <- sample(values, y)
    # Step 3:
    # Compute the correlation between x and the randomly mixed
    # up y-vector. Store this value in the vector from step 1.
   correlation_value <- cor.test(x, y)
   means[i] <- correlation_values
  }
  
  # Step 4:
  # Return new updated vector, created in step 1
  means
}
```

2. Create Plots that Visually show result of these statistical tests on your two questions.

3. Conclusion 
a. Use percentiles, summary statistics (max, min), and probabilites (p-values)






