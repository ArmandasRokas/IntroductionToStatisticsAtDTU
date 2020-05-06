# 3 Confidence Intervals

## 3.1 Concrete items

> A construction company receives concrete items for a construction. The length
> of the items are assumed reasonably normally distributed. The following requirements
> for the length of the elements are made $\mu=3000mm$. The company samples 9 items from a delivery which are then measured for control. The following measurements (in mm) are found: 3003, 3005, 2997, 3006, 2999, 2998, 3007, 3005, 3001.

### a) 

> Compute the following three statistics: the sample mean, the sample standard deviation and the standard error of the mean, and what are the interpretations of these statistics?

$$
\bar{x} = 3002.333 \\
s = 3.708099 \\
SE_{\bar{x}}= \frac{s}{\sqrt{n}} = 1.236033
$$



```r
> sample <- c(3003, 3005, 2997, 3006, 2999, 2998, 3007, 3005, 3001)
> mean <- mean(sample)
[1] 3002.333
> sd <- sd(sample)
[1] 3.708099
> error <- sd/sqrt(9)
[1] 1.236033
```

<!-- Rememeber to answer about interpretation: 
These statistics is computed from an observed sample. Page 134 --> 

### b) 

> In a construction process, 5 concrete items are joined together to a single construction with a length which is then the complete length of the 5 concrete items. It is very important that the length of this new construction is within 15 m plus/minus 1 cm. How often will it happen that such a construction will be more than 1 cm away from the 15 m target (assume that the population mean concrete item length is $\mu$ = 3000 mm and that the population standard deviation is $\sigma$ = 3)?

Find:
$$
 P(14990>L>15010)
$$
We know:
$$
L \sim N(3000,3^2 ) \\
L^{scale} = 5L \\
L^{scale} \sim N(15000, 45)
$$
Solution:
$$
P(14990>L>15010) = 2*P(L<14990) = 0.1360371 \\
$$

```r
> 2*pnorm(14990, mean=15000, sd=sqrt(45)) 
[1] 0.1360371
```

### c)

> Find the 95% confidence interval for the mean $\mu$.

$$
\bar{x}\pm t_{0.975}* \frac{s}{\sqrt{n}} = 3002.333 \pm 2.262*1.236 = \\
= 3002.333 \pm 2.795832 = [ 2999.537,  3005.129]
$$


```R
> qt(0.975,9)
[1] 2.262157
```

### d)

> Find the 99% confidence interval for m. Compare with the 95% one from above and explain why it is smaller/larger!


$$
\bar{x}\pm t_{0.995}* \frac{s}{\sqrt{n}} = 3002.333 \pm 3.249836*1.236 = \\
= 3002.333 \pm 4.016797 = [2998.316,  3006.35]
$$

```R
> qt(0.995,9)
[1] 3.249836
```

- It is larger, because in this case 99% of all CI's should contain the true mean. So that means, if we want a higher likelihood, that the CI contains the population mean, so we should make the CI larger. 

### e)

> Find the 95% confidence intervals for the variance $\sigma^2$ and the standard deviation $\sigma$.

- The 95% CI for the variance:

$$
\left[\frac{(n-1)s^2}{\chi^2_{0.975}}, \frac{(n-1)s^2}{\chi^2_{0.025}}\right] = [6.27333, 50.46495] \\
$$



```R
> (9-1)*var(sample)/qchisq(0.975, df=8)
[1] 6.27333
> (9-1)*var(sample)/qchisq(0.025, df=8)
[1] 50.46495
```

- The 95% CI for the standard deviation: 

$$
\left[\sqrt{6.27333}, \sqrt{50.46495}\right] = [2.504662, 7.103869] \\
$$

### f)

> Find the 99% confidence intervals for the variance $\sigma^2$ and the standard deviation $\sigma$.

- The 99% CI for the variance:

$$
\left[\frac{(n-1)s^2}{\chi^2_{0.995}}, \frac{(n-1)s^2}{\chi^2_{0.005}}\right] = [5.010259, 81.82009] \\
$$

```R
> (9-1)*var(sample)/qchisq(0.995, df=8)
[1] 5.010259
> (9-1)*var(sample)/qchisq(0.005, df=8)
[1] 81.82009
```


- The 99% CI for the standard deviation: 

$$
\left[\sqrt{5.010259}, \sqrt{81.82009}\right] = [2.238361, 9.045446] \\
$$

## 3.2 Aluminum profile

> The length of an aluminum profile is checked by taking a sample of 16 items whose length is measured. The measurement results from this sample are listed below, all measurements are in mm: 180.02, 180.00, 180.01, 179.97, 179.92, 180.05, 179.94, 180.10,180.24, 180.12, 180.13, 180.22, 179.96, 180.10, 179.96, 180.06 . From data is obtained: $\bar{x}=180.05 $ and $s = 0.0959$ . It can be assumed that the sample comes from a population which is normal distributed.

### a) 

> A 90%-confidence interval for $\mu$ becomes?

$$
\bar{x}\pm t_{0.95}* \frac{s}{\sqrt{n}} = 180.05 \pm 1.75305*\frac{0.0959}{\sqrt{16}} = \\
= 180.05 \pm 0.04202937 = [ 180.008,  180.092]
$$



```R
> qt(0.95,15)
[1] 1.75305
```

### b)

> A 99%-confidence interval for $\sigma$ becomes?

$$
\left[\sqrt{\frac{(n-1)s^2}{\chi^2_{0.995}}}, \sqrt{\frac{(n-1)s^2}{\chi^2_{0.005}}}\right] = [0.06485128, 0.1731578] \\
$$

```R
> sqrt((16-1)*0.0959^2/qchisq(0.995, df=15))
[1] 0.06485128
> sqrt((16-1)*0.0959^2/qchisq(0.005, df=15))
[1] 0.1731578
```

