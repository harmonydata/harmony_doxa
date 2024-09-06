# Harmony for Doxa AI challenge

## 1. Matching

I have included an Excel with human judged similarity values between sentences.

There is a Jupyter notebook that calculates Harmony's correlation with the human values, and one that calculates OpenAI's correlation.

In both cases, a linear model means that we predict the human similarity with an average error of 24.

Harmony with the default Huggingface LLM (`sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`) gets R2 = 0.01254, Harmony with OpenAI (`text-embedding-ada-002`) gets R2 = 0.01022

We would like to improve on this, to get something which can better predict the human rated similarity.

Here is a script in R which outputs the R2 score:

```
df <- read.csv("with_openai.csv")
model <- lm(df$human_similarity ~ df$cosine_from_harmony)
summary(model)
```

Outputs:

```
Call:
lm(formula = df$human_similarity ~ df$cosine_from_harmony)

Residuals:
    Min      1Q  Median      3Q     Max 
-31.411 -23.098  -9.247  22.131  79.739 

Coefficients:
                       Estimate Std. Error t value Pr(>|t|)    
(Intercept)             24.3939     0.5885  41.449  < 2e-16 ***
df$cosine_from_harmony  10.3444     1.6939   6.107 1.15e-09 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 27.47 on 2937 degrees of freedom
Multiple R-squared:  0.01254,	Adjusted R-squared:  0.0122 
F-statistic: 37.29 on 1 and 2937 DF,  p-value: 1.151e-09

```


```
df <- read.csv("with_openai.csv")
model <- lm(df$human_similarity ~ df$cosine_openai)
summary(model)
```

Outputs:

```
Call:
lm(formula = df$human_similarity ~ df$cosine_openai)

Residuals:
    Min      1Q  Median      3Q     Max 
-27.791 -26.938  -8.771  22.626  76.001 

Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
(Intercept)       23.0633     0.7657  30.120  < 2e-16 ***
df$cosine_openai   5.3357     0.9690   5.507 3.97e-08 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 27.51 on 2937 degrees of freedom
Multiple R-squared:  0.01022,	Adjusted R-squared:  0.009882 
F-statistic: 30.32 on 1 and 2937 DF,  p-value: 3.973e-08



```


## 2. PDF Parsing

see the accompanying PDF problem description.
