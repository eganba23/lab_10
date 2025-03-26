Lab 10 - Grading the professor, Pt. 2
================
Benjamin Egan
3/25/2025

This is the link to the assignment page
(<https://datascience4psych.github.io/DataScience4Psych/lab10.html>).
This includes the relevant information for the assignment alongside
required questions I needed to answer.

## Simple Linear Regression

``` r
view(evals)

m_bty <- lm(score ~ bty_avg, data = evals)

summary(m_bty)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.9246 -0.3690  0.1420  0.3977  0.9309 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3.88034    0.07614   50.96  < 2e-16 ***
    ## bty_avg      0.06664    0.01629    4.09 5.08e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5348 on 461 degrees of freedom
    ## Multiple R-squared:  0.03502,    Adjusted R-squared:  0.03293 
    ## F-statistic: 16.73 on 1 and 461 DF,  p-value: 5.083e-05

Linear Model: y = 3.88 + .067x <br/> R-squared: .035 <br/> Adjusted
R-squared: .033

## Multiple Linear Regression

``` r
m_bty_gen <- lm(score ~ bty_avg + gender, data = evals)

summary(m_bty_gen)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + gender, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8305 -0.3625  0.1055  0.4213  0.9314 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  3.74734    0.08466  44.266  < 2e-16 ***
    ## bty_avg      0.07416    0.01625   4.563 6.48e-06 ***
    ## gendermale   0.17239    0.05022   3.433 0.000652 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5287 on 460 degrees of freedom
    ## Multiple R-squared:  0.05912,    Adjusted R-squared:  0.05503 
    ## F-statistic: 14.45 on 2 and 460 DF,  p-value: 8.177e-07

Linear model: y = 3.747 + .074(bty_avg) + .172(gender) <br/> R-squared:
.059 <br/> Adjusted R-squared: .055 <br/>

#### Interpretation

intercept: A female with an average beauty rating of zero will get an
evaluation of 3.7

bty_avg slope: For people of the same gender, increasing their average
beauty rating by one will only increase their evaluation score by .07

gender slope: A male will have .172 higher eval score than a female with
the same average beauty rating.

#### Questions 4-9

4.  This model (m_bty_gen) accounts for 5.5% of the variance in score

5.  For males: y = 3.747 + .074(bty_avg) + .172

6.  Males will tend to have the higher beauty rating compared to females

7.  Males have a slightly higher evaluation score (.172) than females
    for the same beauty rating.

8.  m_bty r-squared of .033 versus m_bty_gen r-squared of .055. Adding
    gender to the model only accounts for an additional 2.2% of the
    variance of score. I would say adding it made little difference in
    explaining evaluation scores.

9.  .067 bty_avg slope for the original model. .074 bty_avg slope for
    the model with gender. Adding gender meant that beauty rating of
    professor had a slightly increased “weight” for predicting score.

### Replacing gender with rank

``` r
m_bty_rank <- lm(score ~ bty_avg + rank, data = evals)

summary(m_bty_rank)
```

    ## 
    ## Call:
    ## lm(formula = score ~ bty_avg + rank, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8713 -0.3642  0.1489  0.4103  0.9525 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       3.98155    0.09078  43.860  < 2e-16 ***
    ## bty_avg           0.06783    0.01655   4.098 4.92e-05 ***
    ## ranktenure track -0.16070    0.07395  -2.173   0.0303 *  
    ## ranktenured      -0.12623    0.06266  -2.014   0.0445 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5328 on 459 degrees of freedom
    ## Multiple R-squared:  0.04652,    Adjusted R-squared:  0.04029 
    ## F-statistic: 7.465 on 3 and 459 DF,  p-value: 6.88e-05

Linear model: y = 3.982 + .068(bty_avg) - .161(tenure track) <br/>
Linear model: y = 3.982 + .068(bty_avg) - .126(tenured)

R-squared: .047 Adjusted R-squared: .040

#### Interpretation

intercept: A teaching professor with an average beauty rating of zero
will get an evaluation of 3.98

bty_avg slope: For people of the same rank, increasing their average
beauty rating by one will only increase their evaluation score by .068

tenure track slope: A tenure track professor will have a .161 lower eval
score than a teaching professor with the same average beauty rating.

tenured slope: A tenured professor will have a .126 lower eval score
than a teaching professor with the same average beauty rating.

## Finding the best model

Going forward, I will only consider the following variables as potential
predictors: rank, ethnicity, gender, language, age, cls_perc_eval,
cls_did_eval, cls_students, cls_level, cls_profs, cls_credits, bty_avg.

11. Based on the predictors above, I would guess ethnicity would be the
    worst predictors.

``` r
worst_pred <- lm(score ~ ethnicity, data = evals)

summary(worst_pred)
```

    ## 
    ## Call:
    ## lm(formula = score ~ ethnicity, data = evals)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8912 -0.3816  0.1088  0.4088  0.9281 
    ## 
    ## Coefficients:
    ##                       Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            4.07187    0.06786  60.003   <2e-16 ***
    ## ethnicitynot minority  0.11935    0.07310   1.633    0.103    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5429 on 461 degrees of freedom
    ## Multiple R-squared:  0.005749,   Adjusted R-squared:  0.003593 
    ## F-statistic: 2.666 on 1 and 461 DF,  p-value: 0.1032

The Adjusted R-squared value is .0035, meaning that ethnicity accounts
for around .35% of the variance in score

13. Since I’m already including the percent of students completing the
    eval and the total number of students, I think it wouldn’t make
    sense to include cls_did_eval (number of students who completed the
    eval). The information is already conveyed by the other two
    variables, and this addition would be redundant.

#### Figuring out best model

``` r
evals$ethnicity_relevel <- relevel(evals$ethnicity, ref = "not minority")

all_pred <- lm(score ~ rank + ethnicity + gender + language + age + cls_perc_eval + cls_students + cls_level + cls_profs + cls_credits + bty_avg, data = evals)

summary(all_pred)
```

    ## 
    ## Call:
    ## lm(formula = score ~ rank + ethnicity + gender + language + age + 
    ##     cls_perc_eval + cls_students + cls_level + cls_profs + cls_credits + 
    ##     bty_avg, data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.84482 -0.31367  0.08559  0.35732  1.10105 
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.5305036  0.2408200  14.660  < 2e-16 ***
    ## ranktenure track      -0.1070121  0.0820250  -1.305 0.192687    
    ## ranktenured           -0.0450371  0.0652185  -0.691 0.490199    
    ## ethnicitynot minority  0.1869649  0.0775329   2.411 0.016290 *  
    ## gendermale             0.1786166  0.0515346   3.466 0.000579 ***
    ## languagenon-english   -0.1268254  0.1080358  -1.174 0.241048    
    ## age                   -0.0066498  0.0030830  -2.157 0.031542 *  
    ## cls_perc_eval          0.0056996  0.0015514   3.674 0.000268 ***
    ## cls_students           0.0004455  0.0003585   1.243 0.214596    
    ## cls_levelupper         0.0187105  0.0555833   0.337 0.736560    
    ## cls_profssingle       -0.0085751  0.0513527  -0.167 0.867458    
    ## cls_creditsone credit  0.5087427  0.1170130   4.348  1.7e-05 ***
    ## bty_avg                0.0612651  0.0166755   3.674 0.000268 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.504 on 450 degrees of freedom
    ## Multiple R-squared:  0.1635, Adjusted R-squared:  0.1412 
    ## F-statistic: 7.331 on 12 and 450 DF,  p-value: 2.406e-12

``` r
evals$ethnicity_relevel <- relevel(evals$ethnicity, ref = "not minority")

best_model <- lm(score ~  ethnicity_relevel + gender + language + age + cls_perc_eval + cls_students + cls_credits + bty_avg, data = evals)

summary(best_model)
```

    ## 
    ## Call:
    ## lm(formula = score ~ ethnicity_relevel + gender + language + 
    ##     age + cls_perc_eval + cls_students + cls_credits + bty_avg, 
    ##     data = evals)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.89519 -0.31227  0.08596  0.37022  1.09853 
    ## 
    ## Coefficients:
    ##                             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                3.5907568  0.1977629  18.157  < 2e-16 ***
    ## ethnicity_relevelminority -0.2044482  0.0746764  -2.738 0.006428 ** 
    ## gendermale                 0.1768250  0.0503142   3.514 0.000485 ***
    ## languagenon-english       -0.1511723  0.1035293  -1.460 0.144930    
    ## age                       -0.0048725  0.0026073  -1.869 0.062298 .  
    ## cls_perc_eval              0.0057538  0.0015405   3.735 0.000212 ***
    ## cls_students               0.0004073  0.0003428   1.188 0.235355    
    ## cls_creditsone credit      0.5230953  0.1050306   4.980 9.03e-07 ***
    ## bty_avg                    0.0618985  0.0165267   3.745 0.000203 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5028 on 454 degrees of freedom
    ## Multiple R-squared:  0.1602, Adjusted R-squared:  0.1454 
    ## F-statistic: 10.82 on 8 and 454 DF,  p-value: 5.463e-14

Final model: y = .20(ethnicity) + .177(gender) - .151(language) -
.005(age) + .005(cls_perc_eval) + .000(cls_students) +
.523(cls_credits) + .062(bty_avg)

#### Interpretations

Beauty Average: holding all other variables constant, a 1 point increase
in beauty rating corresponds with a .062 increase in score.

Ethnicity: holding all other variables constant, minority professors see
a .204 decrease in evaluation score compared to non-minority professors

#### The ideal professor

A high scoring professor would be a teaching non-minority male
professor. He would speak English, teach a multiple credit course, and
have a high average beauty rating.

18. I would say no. As it stands, the current model accounts for roughly
    15% of the variance in evaluation scores. Variables I would want to
    factor in are things like the number of years teaching, subject of
    the course material, how long the professor has been teaching that
    specific course, etc. I think these would be variables that greatly
    impact the current model and can provide additional explanation for
    the variance in professor scores.
