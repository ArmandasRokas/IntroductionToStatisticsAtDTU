# Categorical and Count Data

## 7.1 Passing proportions

> The passing proportions for the two courses, $p_1$ and $p_2$ should be compared. 



|                | Course 1 | Course 2 | *Row total* |
| -------------- | -------- | -------- | ----------- |
| Passed         | 82       | 104      | 186         |
| Not passed     | 26       | 39       | 65          |
| *Column total* | 108      | 143      | 251         |

### a) 

> Compute a 95% confidence interval for the difference between the two passing proportions. 

 **By Method 7.15**
$$
\hat{p_1} = \frac{82}{108} = 0.7592593 \\
\hat{p_2} = \frac{104}{143} = 0.7272727
$$

$$
\hat{\sigma}_{\hat{p_1} -\hat{p_2}} = \sqrt{\frac{\hat{p_1}(1-\hat{p_1})}{n_1}+\frac{\hat{p_2}(1-\hat{p_2})}{n_2}} = 0.05549318
$$

```R
n1 <- 108
n2 <- 143
p1 <- 82/n1
p2 <- 104/n2

SEp1 <- sqrt(p1*(1-p1)/n1) 
SEp2 <- sqrt(p2*(1-p2)/n2)
SEp1p2 <- sqrt(SEp1^2+SEp2^2)
SEp1p2
0.05549318
```



- So the 95% CI for the difference is: 


$$
(\hat{p}_1-\hat{p}_2) \pm z_{1-\alpha/2}*\hat\sigma_{\hat{p}_1-{\hat{p}_2}} = [-0.0767781,0.1407512 ]
$$


```R
(p1-p2) - qnorm(1-0.05/2) * SEp1p2
-0.0767781
(p1-p2) + qnorm(1-0.05/2) * SEp1p2
0.1407512
```



**By `prop.test` function**

```R
> prop.test(x=c(82,104), n=c(n1,n2), correct=FALSE)

	2-sample test for equality of proportions without continuity correction

data:  c(82, 104) out of c(n1, n2)
X-squared = 0.32805, df = 1, p-value = 0.5668
alternative hypothesis: two.sided
95 percent confidence interval:
 -0.0767781  0.1407512
sample estimates:
   prop 1    prop 2 
0.7592593 0.7272727 
```





### b) 

> What is the critical values for the $\chi^2$-test of the hypothesis $H_0:p_1=p_2$ with significance level $\alpha= 0.01$ ?

**By method 7.22**

- The degree of freedom is  $(r-1)(c-1) = (2-1)(2-1) = 1$ 

```R
> qchisq(1-0.01, df=1)
[1] 6.634897
```



!!! Note

​	$z_{1-\alpha/2}$, but $\chi^2_{1-\alpha}$ . So you don't divide $\alpha$ by two, when you use $\chi^2$  distribution.



### c)

>  If the passing proportion for a course given repeatedly is assumed to be 0.80 on average, and there are 250 students who are taking the exam each time, what is the expected value, $\mu$ and standard deviation $\sigma$, for the number of students who **do not pass** the exam for a randomly selected course?

**By Theorem 2.21**


$$
\mu = np = 250 * 0.20  = 50 \\
\sigma = \sqrt{np(1-p)} = \sqrt{250*0.2(1-0.2)} =  6.324555
$$


## 7.2 Outdoor lighting

> A company that sells outdoor lighting, gets a lamp produced in 3 material variations: in copper, with painted surface and with stainless steel. The lamps are sold partly in Denmark and partly for export. For 250 lamps the distribution of sales between the three variants and Denmark/export are depicted. The data is shown in the following table:

|                         | Denmark (Success?) | Export (Failure?) |
| ----------------------- | ------------------ | ----------------- |
| Copper variant          | 7.2%               | 6.4%              |
| Painted variant         | 28.0%              | 34.8%             |
| Stainless steel variant | 8.8%               | 14.8%             |

### a)

> Is there a significant difference between the proportion exported and the proportion sold in Denmark (with $\alpha = 0.05$)?
>

- Here we need to find difference between Denmark and export, which means that we don't need to specify different variants. So the total number for Denmark and the total number for export is respectively 44% and 56% or 110 lamps and 140 lamps.



**By method 7.11 (One sample proportion hypothesis test) :**


$$
H_0: {p} = 0.5 \\
H_1:  {p} \ne 0.5
$$

$$
z_{obs} = \frac{x-np_0}{\sqrt{np_0(1-p_0)}} = -1.897367
$$

$$
\text{p-value} =   0.05777957
$$

```R
> zobs <- (110 - 250*0.5)/(sqrt(250*0.5*(0.5)))
[1] -1.897367
> pvalue <- 2* (1-pnorm(abs(zobs)))
[1] 0.05777957
```



- $\text{p-value} > \alpha$ , so we accept $H_0$, meaning that there is no significant difference between the proportion exported and the proportion sold in Denmark. 

**With `prop.test`**

```R
> prop.test(x= xDK, n = n, p = 0.5, correct=FALSE)

	1-sample proportions test without continuity correction

data:  xDK out of n, null probability 0.5
X-squared = 3.6, df = 1, p-value = 0.05778
alternative hypothesis: true p is not equal to 0.5
95 percent confidence interval:
 0.379837 0.501979
sample estimates:
   p 
0.44 
```



### b)

> The relevant critical value to use for testing whether there is a significant difference in how the sold variants are distributed in Denmark and for export is (with $\alpha = 0.05$)?

- The degree of freedom:  $ (R-1)(C-1) = (3-1)(2-1) = 2$
- The correct answer is:

$$
\chi^2_{1-\alpha}=   \chi^2_{0.95}  =   5.991465
$$

```R
qchisq(0.95, df=2)
```



## 7.3 Local election

> At the local elections in Denmark in November 2013 the Social Democrats (A) had $p = 29.5\%$ of the votes at the country level. From an early so-called exit poll it was estimated that they would only get $22.7\%$ of the votes. Suppose the exit poll was based on $740$ people out of which then $168$ people reported having voted for A.



### a)
>  At the time of the exit poll the $p$ was of course not known. If the following
hypothesis was tested based on the exit poll:

$$
H_0: p = 0.295 \\
H_1 : p \ne 0.295
$$

> what test statistic and conclusion would then be obtained with $\alpha=0.001$? 

- **Test statistic**

$$
z_{obs} = \frac{x-np_0}{\sqrt{np_0(1-p_0)}} \\
x = 168 \\
n = 740 \\
p_0 = 0.295
$$



```R
>   n <- 740
>   x <- 168
>   p0 <- 0.295
>   zobs <- (x - n*p0)/(sqrt(n*p0*(1-p0)))
[1] -4.054586
```

So we get that
$$
z_{obs} = -4.054586
$$

- **The critical value**

$$
z_{1-\alpha/2} 
$$

```R
> qnorm(1-(0.001/2))
3.290527
```



- **Conclusion**

$|z_{obs}| = 4.0545$ is more than the critical value $3.290527$, so we reject $H_0$. This means that it was significantly unlikely that Social Democrats would have $p=29.5$ at the local elections in Denmark in November 2013 based on the exit poll. 



### b)

> Calculate a 95%-confidence interval for $p$ based on the exit poll.

**By method 7.3:**


$$
\hat{p} \pm z_{1-\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}
$$

Where
$$
n = 740 \\
\hat{p} = 0.227 \\
z_{1-0.05/2} = 1.959964
$$
So  the answer is:
$$
0.227 \pm 0.03018109 = [0.1968189, 0.2571811 ]
$$
or
$$
[19.7\%, 25.7\%]
$$

**With `prop.test`**

```R
> prop.test(x=168 , n=740 , p=0.295, correct=FALSE)

	1-sample proportions test without continuity correction

data:  168 out of 740, null probability 0.295
X-squared = 16.44, df = 1, p-value = 5.022e-05
alternative hypothesis: true p is not equal to 0.295
95 percent confidence interval:
 0.1982994 0.2585741
sample estimates:
       p 
0.227027 
```








## 7.4

> A wholesaler needs to find a supplier that delivers sugar in 1 kg bags. From two potential suppliers 50 bags of sugar are received from each. A bag is described as ’defective’ if the weight of the filled bag is less than 990 grams. The received bags were all control weighed and 6 defective from supplier A and 12 defective from supplier B were found.

### a)

> If the following hypothesis

$$
H_0 : p_A = p_B, \\
H_1 : p_A \ne p_B
$$

> is tested on a significance level of 5%, what is the p-value and conclusion?

- Given:

$$
x_{A} = 6 \\
x_{B} = 12 \\
n_A = n_B = 50 \\
\hat{p}_A = 0.12 \\
\hat{p}_B = 0.24
$$


**By method 7.18**


$$
\hat{p} = \frac{x_A + x_B}{n_A+n_B} = 0.18
$$

- Test statics

$$
z_{obs} = \frac{\hat{p}_A -\hat{p}_B }{\sqrt{\hat{p}(1-\hat{p})(\frac{1}{n_A}+\frac{1}{n_A})}} = -1.561738
$$

- Critical value


$$
z_{1-\alpha/2} = z_{0.975} = 1.959964
$$

- Conclusion

$|z_{obs}| = 1.561738$ is less than the critical value, so we accept $H_0$, which means that there is no significant difference between two suppliers. 

**With  `prop.test` and `chisq.test`**

```R
> prop.test(x=c(6,12), n=c(50,50), correct = FALSE, conf.level = 0.95)

	2-sample test for equality of proportions without continuity correction

data:  c(6, 12) out of c(50, 50)
X-squared = 2.439, df = 1, p-value = 0.1183
alternative hypothesis: two.sided
95 percent confidence interval:
 -0.26875081  0.02875081
sample estimates:
prop 1 prop 2 
  0.12   0.24 

> chisq.test(matrix(c(6,12,44,38), ncol = 2), correct = FALSE)

	Pearsons Chi-squared test

data:  matrix(c(6, 12, 44, 38), ncol = 2)
X-squared = 2.439, df = 1, p-value = 0.1183
```



### b)

> A supplier has delivered 200 bags, of which 36 were defective. A 99% confidence interval for $p$ the proportion of defective bags for this supplier is:

$$
\hat{p} \pm z_{1-\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}
$$

Where
$$
n = 200 \\
\hat{p} = \frac{36}{200} = 0.18 \\
z_{1-0.01/2} = 2.575829
$$
So  the answer is:
$$
0.18 \pm 0.03637847 = [ 0.11, 0.25 ]
$$
or
$$
[22,50 ]
$$

```R
> n <- 200
> p <- 36/200
> z <- qnorm(1-0.01/2)
> p - z * sqrt(p*(1-p)/n)
[1] 0.1100246
> p + z * sqrt(p*(1-p)/n)
[1] 0.2499754
```



**With `prop.test`**

```R
> prop.test(x=36, n=200, correct=FALSE, conf.level=0.99)

	1-sample proportions test without continuity correction

data:  36 out of 200, null probability 0.5
X-squared = 81.92, df = 1, p-value < 2.2e-16
alternative hypothesis: true p is not equal to 0.5
99 percent confidence interval:
 0.1206696 0.2598803
sample estimates:
   p 
0.18 
```



## 7.5

> A company wants to investigate whether the employees’ physical training condition will affect their success in the job. 200 employees were tested and the following count data were found:



|                         |                   | Physical training condition |                   |         |
| ----------------------- | ----------------- | --------------------------- | ----------------- | ------- |
|                         | **Below average** | **Average**                 | **Above average** | *Total* |
| **Bad job success**     | 11                | 27                          | 15                | 53      |
| **Average job success** | 14                | 40                          | 30                | 84      |
| **Good job success**    | 5                 | 23                          | 35                | 63      |
| *Total*                 | 30                | 90                          | 80                | 200     |

> The hypothesis of independence between job success and physical training condition is to be tested by the use of the for this setup usual $\chi^2$−test.

### a)

> What is the expected number of individuals with above average training condition and good job success under $H_0$ (i.e. if $H_0$ is assumed to be true)?

- The expected number under the null hypothesis for each cell is found as

$$
e_{ij} = "j\text{th column total}" * \frac{"i\text{th row total}"}{"\text{grand total}"}
$$

*  The answer for table cell(3,3) is


$$
e_{33} =  80 * 63 / 200 = 25.2
$$


### b)

> For the calculation of the relevant $\chi^2$-test statistic, identify the following two numbers: 

- **A:**

The number of contributions to the test statistic: 
 $R*C = 3*3 = 9 $, one for each cell 



- **B:**


$$
  \frac{(o_{11}-e_{11})^2}{e_{11}}
$$

 Find $o_{ii}$ and $e_{ii}$

$$
o_{11} = 11 \\
e_{11} = 30*53/200 = 7.95
$$

Hence

$$
\frac{(11-7.95)^2}{7.95} = 1.170126
$$

- So the contribution to the statistic from table cell (1,1) is $1.170126$




### c) 

> The total $\chi^2$-test statistic is $10.985$, so the $\text{p-value}$ and the conclusion will be(both must be valid):



- The degree of freedom: $(R-1)(C-1)= (3-1)(3-1) = 2$

```R
> pvalue <- 1 - pchisq(10.985, df=4)
[1] 0.02673311
```

- So $\text{p-value} = 0.0267$

- The conclusion is that the calculated $\text{p-value}$ is less than $\alpha=0.05$, which means that the hypothesis of **independence** between physical training condition and success in the job is **rejected** on a 5% level. In other words, there is significant dependence between job success and physical training condition.

<!-- What about significance level $\alpha$ here? Do we need choose it by ourself? -->

```R
> training <- matrix(c(11,27,15,14,40,30,5,23,35), ncol = 3, byrow = TRUE)
> colnames(training)  <- c("Below averga", "Average", "Above average")
> rownames(training) <- c("Bad job success", "Average job success", "Good job success")
> training
                    Below averga Average Above average
Bad job success               11      27            15
Average job success           14      40            30
Good job success               5      23            35
> chi <- chisq.test(training, correct = FALSE)
> chi

	Pearsons Chi-squared test

data:  training
X-squared = 10.985, df = 4, p-value = 0.02673
```

