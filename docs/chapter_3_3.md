# Analysis of Two Samples

## Exercise 3.6 Cholesterol

> In a clinical trial of a cholesterol-lowering agent, 15 patients’ cholesterol (in mmol/L) has been measured before treatment and 3 weeks after starting treatment. Data are listed in the following table:

| Patient | Before | After |
| ------- | ------ | ----- |
| 1       | 9.1    | 8.2   |
| 2       | 8.0    | 6.4   |
| 3       | 7.7    | 6.6   |
| 4       | 10.0   | 8.5   |
| 5       | 9.6    | 8.0   |
| 6       | 7.9    | 5.8   |
| 7       | 9.0    | 7.8   |
| 8       | 7.1    | 7.2   |
| 9       | 8.3    | 6.7   |
| 10      | 9.6    | 9.8   |
| 11      | 8.2    | 7.1   |
| 12      | 9.2    | 7.7   |
| 13      | 7.3    | 6.0   |
| 14      | 8.5    | 6.6   |
| 15      | 9.5    | 8.4   |

The following is run in R:

```R
x1 <- c(9.1, 8.0, 7.7, 10.0, 9.6, 7.9, 9.0, 7.1, 8.3,
9.6, 8.2, 9.2, 7.3, 8.5, 9.5)
x2 <- c(8.2, 6.4, 6.6, 8.5, 8.0, 5.8, 7.8, 7.2, 6.7,
9.8, 7.1, 7.7, 6.0, 6.6, 8.4)

t.test(x1, x2)
Welch Two Sample t-test
data: x1 and x2
t = 3.3, df = 27, p-value = 0.003
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
0.4637 1.9630
sample estimates:
mean of x mean of y
8.600 7.387

t.test(x1, x2, pair=TRUE)
Paired t-test
data: x1 and x2
t = 7.3, df = 14, p-value = 0.000004
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
0.8588 1.5678
sample estimates:
mean of the differences
1.213
```

### a)

> Can there, based on these data be demonstrated a significant decrease in cholesterol levels with $\alpha$ = 0.001?

This is clearly a **paired** setting, because the same persons were measured before treatment and 3 weeks after starting treatment. So only the results from the last of the R-calls are relevant, where we can read off the results:

 The (non-directional) $\text{p-value}= 0.00000367$, so there is very strong evidence against the null hypothesis, and we can beyond any reasonable doubts conclude that the mean cholesterol level has decreased after the 3 weeks.



## 3.7 Pulse

| Runner | Pulse end | Pulse 1min |
| ------ | --------- | ---------- |
| 1      | 173       | 120        |
| 2      | 175       | 115        |
| 3      | 174       | 122        |
| 4      | 183       | 123        |
| 5      | 181       | 125        |
| 6      | 180       | 140        |
| 7      | 170       | 108        |
| 8      | 182       | 133        |
| 9      | 188       | 134        |
| 10     | 178       | 121        |
| 11     | 181       | 130        |
| 12     | 183       | 126        |
| 13     | 185       | 128        |

The following was run in R:

```R
Pulse_end <- c(173,175,174,183,181,180,170,182,188,178,181,183,185)
Pulse_1min <- c(120,115,122,123,125,140,108,133,134,121,130,126,128)
mean(Pulse_end)
[1] 179.5
mean(Pulse_1min)
[1] 125
sd(Pulse_end)
[1] 5.19
sd(Pulse_1min)
[1] 8.406
sd(Pulse_end-Pulse_1min)
[1] 5.768
```



### a)

> What is the 99% confidence interval for the mean pulse drop (meaning the drop during 1 minute from end of workout)?

- We know that these samples are dependent(paired situation), so so we apply the one-sample theory (Method 3.9) on the differences in order to find CI



```R
mean_diff <- mean(Pulse_end) - mean(Pulse_1min)


c(mean_diff - qt(1-0.01/2, df=12)*sd_diff/sqrt(13),
  mean_diff + qt(1-0.01/2, df=12)*sd_diff/sqrt(13))
49.57507 59.34801
```





### b)

> Consider now the 13 pulse end measurements (first row in the table). What is the 95% confidence interval for the standard deviation of these?

By method 3.19
$$
\left[\sqrt{\frac{(n-1)s^2}{\chi_{1-0.05/2}^2}}, \sqrt{\frac{(n-1)s^2}{\chi_{0.05/2}^2}} \right] = [3.721662, 8.567283]
$$


```R
c(sqrt(12*var(Pulse_end)/qchisq(1-0.05/2, df=12)),     sqrt(12*var(Pulse_end)/qchisq(0.05/2, df=12))) 
[1] 3.721662 8.567283
```

- So the answer is that we accept that $\sigma\in[3.721662, 8.567283]$ 





## 3.8 Foil production

> In the production of a certain foil (film), the foil is controlled by measuring the thickness of the foil in a number of points distributed over the width of the foil. The production is considered stable if the mean of the difference between the maximum and minimum measurements does not exceed 0.35 mm. At a given day, the following random samples are observed for 10 foils:



| Foil | Max. in mm $y_{max}$ | Min. in mm $y_{min}$ | Max-Min(D) |
| ---- | -------------------- | -------------------- | ---------- |
| 1    | 2.62                 | 2.14                 | 0.48       |
| 2    | 2.71                 | 2.39                 | 0.32       |
| 3    | 2.18                 | 1.86                 | 0.32       |
| 4    | 2.25                 | 1.92                 | 0.33       |
| 5    | 2.72                 | 2.33                 | 0.39       |
| 6    | 2.34                 | 2.00                 | 0.34       |
| 7    | 2.63                 | 2.25                 | 0.38       |
| 8    | 1.86                 | 1.50                 | 0.36       |
| 9    | 2.84                 | 2.27                 | 0.57       |
| 10   | 2.93                 | 2.37                 | 0.56       |

The following statistics may potentially be used
$$
\bar{y}_{max} = 2.508,\ \bar{y}_{min}= 2.103,\ s_{y_{max}}=0.3373,\\
s_{y_{min}}=0.2834,\ s_D=0.09664
$$

### a) 

> What is a 95% confidence interval for the mean difference? 

Answer:
$$
[0.3358679, 0.4741321]
$$


```R
> c(2.508-2.103 - qt(1-0.05/2, df=9)*0.09664/sqrt(10),
    2.508-2.103 + qt(1-0.05/2, df=9)*0.09664/sqrt(10))
[1] 0.3358679 0.4741321
```

Note: The confidence interval contains those values of the mean difference that we believe in based on the data.



### b)

> How much evidence is there that the mean difference is different from 0.35? State the null hypothesis, t-statistic and p-value for this question.

$$
H_0:\ \mu=0.35 \\
H_1:\ \mu\ne0.35
$$





**By using Method 3.36**

**1.**  
$$
t_{obs}= \frac{\bar{x}-\mu_{0}}{s/\sqrt{n}}=1.799723
$$

```R
> ((2.508-2.103)-0.35)/(0.09664/sqrt(10))
[1] 1.799723
```

**2.** 
$$
\text{p-value}= 2*P(T>|t_{obs}|) =  0.1054369
$$

```r
> 2*(1-pt(1.799723, df=9))
[1] 0.1054369
```

**3.  Conclusion:**

$\text{p-value}$ is 0.1054369, so there is little or evidence against $H_{0}$, which is $\mu=0.35$



## 3.9 Course project 



> At a specific education it was decided to introduce a project, running through the course period, as a part of the grade point evaluation. In order to assess whether it has changed the percentage of students passing the course, the following data was collected:



|                               | Before introduction of project | After introduction of project |
| ----------------------------- | ------------------------------ | ----------------------------- |
| Number of students evaluated  | 50                             | 24                            |
| Number of students failed     | 13                             | 3                             |
| Average grade point $\bar{x}$ | 6.420                          | 7.375                         |
| Sample standard deviation $s$ | 2.205                          | 1.813                         |

### a)

> As it is assumed that the grades are approximately normally distributed in each group, the following hypothesis is tested:

$$
H_{0} \ : \ \mu_{Before}= \mu_{After} \equiv \mu_{Before}-\mu_{After}= 0 \\
H_{1}\ : \ \mu_{Before} \ne \mu_{After} \equiv \mu_{Before}-\mu_{After}\ne 0
$$

> The test statistic, the p-value and the conclusion for this test become?

By method 3.51(Welch):

1. 

$$
t_{obs}= \frac{(\bar{x}_1-\bar{x}_2)-\delta_0}{\sqrt{s_1^2/n_1+s^2_2/n_2}}= -1.973387\\
v = \frac{(\frac{s^2_1}{n_1}+\frac{s^2_2}{n_2})^2}{\frac{(s_1^2/n_1)^2}{n_1-1}+\frac{(s_2^2/n_2)^2}{n_2-1}}= 54.38591
$$



```r
> tobs <- (6.420-7.375)/(sqrt((2.205^2/50)+(1.813^2/24)))
[1] -1.973387
> v <- ((s1^2/n1)+(s2^2/n2))^2/
  (((s1^2/n1)^2/(n1-1))+((s2^2/n2)^2/(n2-1)))
[1] 54.38591

```



2. 

$$
\text{p-value}= 0.05354164
$$

```R
2*(1-pt(1.973387, df=54.38591))
```

3. Conclusion

On a 5% level we cannot conclude a significant difference in the grade point means before and after. This means that we cannot reject $H_0$





### b)

> A 99% confidence interval for the mean grade point difference is?

By method 3.47:
$$
\bar{x}-\bar{y}\pm t_{1-\alpha/2}*\sqrt{\frac{s_{1}^2}{n_1}+\frac{s^2_{2}}{n_2}} = [-2.2467772,0.3367772]
$$
```r
c(6.420-7.375-qt(1-0.01/2, df=v)*sqrt(2.205^2/50+1.813^2/24), 
  6.420-7.375+qt(1-0.01/2, df=v)*sqrt(2.205^2/50+1.813^2/24))
[1] -2.2467772  0.3367772
```

- The answer: we accept that the mean difference in the interval $[-2.247; 0.337]$

### c) 

> A 95% confidence interval for the grade point standard deviation after the introduction of the project becomes?



By method 3.19
$$
\left[\sqrt{\frac{(n-1)s^2}{\chi_{1-0.05/2}^2}}, \sqrt{\frac{(n-1)s^2}{\chi_{0.05/2}^2}} \right] = [1.409088, 2.543205]
$$


```R
n <- 24
sd <- 1.813
alpha <- 0.05
c(sqrt((n-1)*sd^2/qchisq(1-alpha/2, df=(n-1))),     
  sqrt((n-1)*sd^2/qchisq(alpha/2, df=(n-1)))) 
[1] 1.409088 2.543205
```

- So the answer is that we accept that $\sigma\in[1.409088,  2.543205]$ 

