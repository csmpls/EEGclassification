


## effects on speed

speed ~ bins + length 

---
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                  speed   R-squared:                       0.933
Model:                            OLS   Adj. R-squared:                  0.932
Method:                 Least Squares   F-statistic:                     2894.
Date:                Fri, 30 May 2014   Prob (F-statistic):          3.21e-245
Time:                        16:34:22   Log-Likelihood:                -536.87
No. Observations:                 420   AIC:                             1080.
Df Residuals:                     417   BIC:                             1092.
Df Model:                           2                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
Intercept      1.7195      0.097     17.767      0.000         1.529     1.910
bins           0.0350      0.000     76.071      0.000         0.034     0.036
length        -0.0189      0.015     -1.244      0.214        -0.049     0.011
==============================================================================
Omnibus:                      108.118   Durbin-Watson:                   0.596
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              292.127
Skew:                          -1.232   Prob(JB):                     3.68e-64
Kurtosis:                       6.260   Cond. No.                         337.
==============================================================================


so..... 3.5x faster 






speed ~ bins + length + subject
---
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                  speed   R-squared:                       0.934
Model:                            OLS   Adj. R-squared:                  0.933
Method:                 Least Squares   F-statistic:                     1951.
Date:                Fri, 30 May 2014   Prob (F-statistic):          1.45e-244
Time:                        16:37:54   Log-Likelihood:                -534.25
No. Observations:                 420   AIC:                             1076.
Df Residuals:                     416   BIC:                             1093.
Df Model:                           3                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
Intercept      1.6209      0.106     15.362      0.000         1.413     1.828
bins           0.0350      0.000     76.456      0.000         0.034     0.036
length        -0.0189      0.015     -1.250      0.212        -0.049     0.011
subject        0.0329      0.014      2.288      0.023         0.005     0.061
==============================================================================
Omnibus:                      104.555   Durbin-Watson:                   0.605
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              273.252
Skew:                          -1.204   Prob(JB):                     4.61e-60
Kurtosis:                       6.133   Cond. No.                         369.
==============================================================================



same........and we're sure...............3.5x increase in time for each bin decreased!!!




## effects of bins/length on bestcase





bestcase ~ bins + lengths
---

*pandas OLS:*

Number of Observations:         1470
Number of Degrees of Freedom:   3

R-squared:         0.0826
Adj R-squared:     0.0814

Rmse:              0.0604

F-stat (2, 1467):    66.0804, p-value:     0.0000

Degrees of Freedom: model 2, resid 1467

  Variable       Coef    Std Err     t-stat    p-value    CI 2.5%   CI 97.5%
------------------------------------------------------------------------------
      bins     0.0001     0.0000       5.21     0.0000     0.0000     0.0001
    length     0.0058     0.0006      10.18     0.0000     0.0047     0.0069
 intercept     0.9076     0.0033     271.83     0.0000     0.9011     0.9142


*statmosdel OLS*:

                             OLS Regression Results                            
==============================================================================
Dep. Variable:               bestcase   R-squared:                       0.066
Model:                            OLS   Adj. R-squared:                  0.065
Method:                 Least Squares   F-statistic:                     103.2
Date:                Fri, 30 May 2014   Prob (F-statistic):           1.77e-23
Time:                        11:24:31   Log-Likelihood:                 2029.3
No. Observations:                1470   AIC:                            -4055.
Df Residuals:                    1468   BIC:                            -4044.
Df Model:                           1                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
const          0.9154      0.003    303.344      0.000         0.909     0.921
length         0.0058      0.001     10.159      0.000         0.005     0.007
==============================================================================
Omnibus:                      245.745   Durbin-Watson:                   2.121
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              398.063
Skew:                          -1.105   Prob(JB):                     3.65e-87
Kurtosis:                       4.271   Cond. No.                         10.3
==============================================================================











>>> y, X = dmatrices('bestcase ~ bins + length + subject', data=df, return_type='dataframe')
>>> mod = sm.OLS(y,X)
>>> res = mod.fit()
>>> print res.summary()
                            OLS Regression Results                            
==============================================================================
Dep. Variable:               bestcase   R-squared:                       0.156
Model:                            OLS   Adj. R-squared:                  0.154
Method:                 Least Squares   F-statistic:                     90.33
Date:                Fri, 30 May 2014   Prob (F-statistic):           1.23e-53
Time:                        14:08:55   Log-Likelihood:                 2104.0
No. Observations:                1470   AIC:                            -4200.
Df Residuals:                    1466   BIC:                            -4179.
Df Model:                           3                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
Intercept      0.9352      0.004    231.988      0.000         0.927     0.943
bins        5.593e-05   1.03e-05      5.428      0.000      3.57e-05  7.61e-05
length         0.0058      0.001     10.609      0.000         0.005     0.007
subject       -0.0039      0.000    -11.288      0.000        -0.005    -0.003
==============================================================================
Omnibus:                      189.312   Durbin-Watson:                   2.202
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              277.035
Skew:                          -0.931   Prob(JB):                     6.96e-61
Kurtosis:                       4.028   Cond. No.                         546.
==============================================================================





y, X = dmatrices('bestcase ~ bins + length + subject + taskpair', data=df, return_type='dataframe')


===================================================================================================
                                      coef    std err          t      P>|t|      [95.0% Conf. Int.]
---------------------------------------------------------------------------------------------------
Intercept                           0.9261      0.005    188.805      0.000         0.917     0.936
taskpair[T.('base', 'eye')]        -0.0029      0.007     -0.435      0.664        -0.016     0.010
taskpair[T.('base', 'finger')]     -0.1070      0.054     -1.974      0.049        -0.213    -0.001
taskpair[T.('base', 'pass')]       -0.0362      0.013     -2.860      0.004        -0.061    -0.011
taskpair[T.('base', 'song')]        0.0448      0.008      5.718      0.000         0.029     0.060
taskpair[T.('base', 'sport')]      -0.0375      0.013     -2.813      0.005        -0.064    -0.011
taskpair[T.('color', 'eye')]        0.0417      0.007      5.977      0.000         0.028     0.055
taskpair[T.('color', 'finger')]     0.0062      0.007      0.911      0.363        -0.007     0.020
taskpair[T.('color', 'pass')]       0.0114      0.004      2.619      0.009         0.003     0.020
taskpair[T.('color', 'song')]       0.0222      0.005      4.121      0.000         0.012     0.033
taskpair[T.('color', 'sport')]      0.0329      0.008      3.982      0.000         0.017     0.049
taskpair[T.('eye', 'finger')]      -0.0522      0.011     -4.727      0.000        -0.074    -0.031
taskpair[T.('eye', 'pass')]         0.0010      0.012      0.084      0.933        -0.022     0.024
taskpair[T.('eye', 'song')]        -0.0120      0.021     -0.576      0.565        -0.053     0.029
taskpair[T.('eye', 'sport')]       -0.0317      0.010     -3.184      0.001        -0.051    -0.012
taskpair[T.('finger', 'pass')]     -0.0055      0.027     -0.200      0.841        -0.059     0.048
taskpair[T.('finger', 'song')]     -0.0356      0.013     -2.806      0.005        -0.060    -0.011
taskpair[T.('finger', 'sport')]    -0.0857      0.020     -4.350      0.000        -0.124    -0.047
taskpair[T.('pass', 'song')]        0.0222      0.009      2.548      0.011         0.005     0.039
taskpair[T.('pass', 'sport')]       0.0003      0.012      0.029      0.977        -0.023     0.023
taskpair[T.('song', 'sport')]      -0.0770      0.025     -3.129      0.002        -0.125    -0.029
bins                             5.152e-05   9.73e-06      5.294      0.000      3.24e-05  7.06e-05
length                              0.0060      0.001     11.239      0.000         0.005     0.007
subject                            -0.0039      0.000    -10.634      0.000        -0.005    -0.003
==============================================================================
Omnibus:                      181.859   Durbin-Watson:                   2.051
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              279.658
Skew:                          -0.866   Prob(JB):                     1.88e-61
Kurtosis:                       4.250   Cond. No.                     7.84e+03
==============================================================================









X = bins
y = bestcase

                            OLS Regression Results                            
==============================================================================
Dep. Variable:               bestcase   R-squared:                       0.488
Model:                            OLS   Adj. R-squared:                  0.488
Method:                 Least Squares   F-statistic:                     1403.
Date:                Fri, 30 May 2014   Prob (F-statistic):          4.47e-216
Time:                        11:41:10   Log-Likelihood:                -1507.7
No. Observations:                1470   AIC:                             3017.
Df Residuals:                    1469   BIC:                             3023.
Df Model:                           1                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
bins           0.0032   8.65e-05     37.452      0.000         0.003     0.003
==============================================================================
Omnibus:                      320.042   Durbin-Watson:                   0.070
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              556.390
Skew:                          -1.436   Prob(JB):                    1.52e-121
Kurtosis:                       3.912   Cond. No.                         1.00
==============================================================================










X = length
y = bestcase

                            OLS Regression Results                            
==============================================================================
Dep. Variable:               bestcase   R-squared:                       0.066
Model:                            OLS   Adj. R-squared:                  0.065
Method:                 Least Squares   F-statistic:                     103.2
Date:                Fri, 30 May 2014   Prob (F-statistic):           1.77e-23
Time:                        13:34:27   Log-Likelihood:                 2029.3
No. Observations:                1470   AIC:                            -4055.
Df Residuals:                    1468   BIC:                            -4044.
Df Model:                           1                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
const          0.9154      0.003    303.344      0.000         0.909     0.921
length         0.0058      0.001     10.159      0.000         0.005     0.007
==============================================================================
Omnibus:                      245.745   Durbin-Watson:                   2.121
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              398.063
Skew:                          -1.105   Prob(JB):                     3.65e-87
Kurtosis:                       4.271   Cond. No.                         10.3
==============================================================================










## effects on average







>>> y, X = dmatrices('avg ~ bins + length + subject', data=df, return_type='dataframe')
>>> mod = sm.OLS(y,X)
>>> res = mod.fit()
>>> print res.summary()
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                    avg   R-squared:                       0.279
Model:                            OLS   Adj. R-squared:                  0.277
Method:                 Least Squares   F-statistic:                     188.9
Date:                Fri, 30 May 2014   Prob (F-statistic):          1.50e-103
Time:                        14:07:13   Log-Likelihood:                 2054.6
No. Observations:                1470   AIC:                            -4101.
Df Residuals:                    1466   BIC:                            -4080.
Df Model:                           3                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
Intercept      0.6402      0.004    153.546      0.000         0.632     0.648
bins        7.204e-05   1.07e-05      6.760      0.000      5.11e-05  9.29e-05
length         0.0117      0.001     20.699      0.000         0.011     0.013
subject       -0.0034      0.000     -9.420      0.000        -0.004    -0.003
==============================================================================
Omnibus:                       29.557   Durbin-Watson:                   1.860
Prob(Omnibus):                  0.000   Jarque-Bera (JB):               31.066
Skew:                           0.355   Prob(JB):                     1.79e-07
Kurtosis:                       2.956   Cond. No.                         546.
==============================================================================











ols(y=df['avg'], x=df[['bins','length']])
---

Number of Observations:         1470
Number of Degrees of Freedom:   3

R-squared:         0.2351
Adj R-squared:     0.2341

Rmse:              0.0617

F-stat (2, 1467):   225.4712, p-value:     0.0000

Degrees of Freedom: model 2, resid 1467

  Variable       Coef    Std Err     t-stat    p-value    CI 2.5%   CI 97.5%
------------------------------------------------------------------------------
      bins     0.0001     0.0000       6.57     0.0000     0.0001     0.0001
    length     0.0117     0.0006      20.11     0.0000     0.0105     0.0128
 intercept     0.6163     0.0034     180.69     0.0000     0.6097     0.6230



                            OLS Regression Results                            
==============================================================================
Dep. Variable:                    avg   R-squared:                       0.213
Model:                            OLS   Adj. R-squared:                  0.212
Method:                 Least Squares   F-statistic:                     396.4
Date:                Fri, 30 May 2014   Prob (F-statistic):           2.80e-78
Time:                        11:26:10   Log-Likelihood:                 1990.1
No. Observations:                1470   AIC:                            -3976.
Df Residuals:                    1468   BIC:                            -3966.
Df Model:                           1                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
const          0.6263      0.003    202.092      0.000         0.620     0.632
length         0.0117      0.001     19.911      0.000         0.011     0.013
==============================================================================
Omnibus:                       12.880   Durbin-Watson:                   1.809
Prob(Omnibus):                  0.002   Jarque-Bera (JB):               12.618
Skew:                           0.202   Prob(JB):                      0.00182
Kurtosis:                       2.792   Cond. No.                         10.3
==============================================================================











X = bins
y = avg

                            OLS Regression Results                            
==============================================================================
Dep. Variable:                    avg   R-squared:                       0.493
Model:                            OLS   Adj. R-squared:                  0.492
Method:                 Least Squares   F-statistic:                     1427.
Date:                Fri, 30 May 2014   Prob (F-statistic):          1.01e-218
Time:                        11:42:00   Log-Likelihood:                -1025.4
No. Observations:                1470   AIC:                             2053.
Df Residuals:                    1469   BIC:                             2058.
Df Model:                           1                                         
==============================================================================
                 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------
bins           0.0024   6.23e-05     37.770      0.000         0.002     0.002
==============================================================================
Omnibus:                      310.853   Durbin-Watson:                   0.084
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              532.662
Skew:                          -1.400   Prob(JB):                    2.16e-116
Kurtosis:                       3.924   Cond. No.                         1.00
==============================================================================
