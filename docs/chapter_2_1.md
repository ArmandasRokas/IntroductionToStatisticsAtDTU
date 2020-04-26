# 2 Probability: Discrete
## 2.1 Discrete random variable

### a) 

> Let X be a stochastic variable. When running the R-command `dbinom(4,10,0.6)` R returns 0.1115, written as:

```R
dbinom(4,10,0.6)
[1] 0.1115
```

> What distribution is applied and what does 0.1115 represent?

- Binomial distribution is applied
- Shows the density or probability of 4 successes in 10 trails with each probability 0.6 

### b)

> Let X be the same stochastic variable as above. The following are results
> from :

```R
pbinom(4,10,0.6)
[1] 0.1662
pbinom(5,10,0.6)
[1] 0.3669
```

> Calculate the following probabilities: P ( X ≤ 5 ) , P ( X < 5 ) , P ( X > 4 ) and
> P ( X = 5 ) .

$$
P(X\leqslant5) = 0.3669\\
P(X < 5 ) = 0.1662 \\
P(X>4) = 1 - P(X < 5 ) = 1 - 0.1662 = 0.8338\\
P(X = 5) = P(X\leqslant5) - P(X < 5 )  = 0.3669 - 0.1662 =  0.2007
$$



### c ) 

> Let X be a stochastic variable. From R we get: 
```R
dpois(4,3)
[1] 0.168
```
> What distribution is applied and what does 0.168 represent?

- Poisson distribution
- The probability of 4 events to happen with rate 3 in given interval. 

### d) 

>Let X be the same stochastic variable as above. The following are results
>from R:

```R
ppois(4,3)
[1] 0.8153
ppois(5,3)
[1] 0.9161
```

> Calculate the following probabilities: P ( X ≤ 5 ) , P ( X < 5 ) , P ( X > 4 ) and
> P ( X = 5 ) .

$$
P(X\leqslant5) = 0.9161 \\
P(X < 5 ) = 0.8153 \\
P(X>4) = 1 - P(X < 5 ) = 1 - 0.8153 = 0.1847 \\
P(X = 5) = P(X\leqslant5) - P(X < 5 )  = 0.9161 - 0.8153 = 0.1008
$$

## 2.4 Consumer survey

> In a consumer survey performed by a newspaper, 20 different groceries (products) were purchased in a grocery store. Discrepancies between the price appearing on the sales slip and the shelf price were found in 6 of these purchased products.

### a) 
> At the same time a customer buys 3 random (different) products within
> the group consisting of the 20 goods in the store. The probability that no
> discrepancies occurs for this customer is?

- Hyper-geometric distribution
- 0 - the desired number of successes (discrepancies)
- 6 - total number of successes (discrepancies) in the population
- 14 - total number of not discrepancies
- 3 - tries without replacement 

```R
> dhyper(0,6, 14, 3)
[1] 0.3192982
```

## 2.5 Hay delivery quality
> A horse owner receives 20 bales of hay in a sealed plastic packaging. To control the hay, 3 bales of hay are randomly selected, and each checked whether it contains harmful fungal spores.
> It is believed that among the 20 bales of hay 2 bales are infected with fungal spores. A random variable X describes the number of infected bales of hay among the three selected.



### a)
> The mean of X, (  $\mu_{X}$ ), the variance of X, ( $\sigma^2_{X}$ ) and P ( X ≥ 1 ) are?

- We know that:
  - Hyper-geometric distribution
  - n  = 3  - draws without replacement 
  - a = 2 - the number of successes in the large population
  - N = 20 - elements in the large population 
- So:   

$$
\mu = n \frac{a}{N}= 3 * \frac{2}{20} = 0.3 \\
\sigma = n \frac{a(N-a)}{N^2}*\frac{N-n}{N-1} = 1.216 \\
P(X \geqslant 1 ) = 1 - P(X = 0) = 1 - 0.7157 = 0.2843
$$



### b)

> Another supplier advertises that no more than 1% of his bales of hay are infected. The horse owner buys 10 bales of hay from this supplier, and decides to buy hay for the rest of the season from this supplier if the 10 bales are error-free. What is the probability that the 10 purchased bales of hay are error-free, if 1% of the bales from a supplier are infected ( $p_{1}$ ) and the probability that the 10 purchased bales of hay are error-free, if 10% of the bales from a supplier are infected ( $p_{10}$ ) ?

The difference from a) is that in a) we picked only 3 from 20 and needed to find probability only in this amount, but here we have probability of event and number of events. 

```R
> dbinom(0,10,0.01)
[1] 0.9043821
> dbinom(0,10,0.1)
[1] 0.3486784
```

## 2.7 A fully automated production

> On a large fully automated production plant items are pushed to a side band at random time points, from which they are automatically fed to a control unit. The production plant is set up in such a way that the number of items sent to the control unit on average is 1.6 item pr. minute. Let the random variable X denote the number of items pushed to the side band in 1 minute. It is assumed that X follows a Poisson distribution. 

### a)

> What is the probability that there will arrive more than 5 items at the control unit in a given minute is?

$$
X \sim Po(\lambda^{min} = 1.6) \\
P(X>5) = 1 - P(X\leqslant  5) = 0.006040291
$$

```R
> 1 - ppois(5, 1.6)
[1] 0.006040291
```

### b)

> What is the probability that no more than 8 items arrive to the control unit
> within a 5-minute period? 

$$
\lambda^{5min} = \lambda{min} * 5 = 1.6 * 5 = 8 \\
P(X \leqslant 8) =  0.5925473
$$

```R
>   ppois(8, 8)
[1] 0.5925473
```

## 2.8 Call center staff
> The staffing for answering calls in a company is based on that there will be 180 phone calls per hour randomly distributed. If there are 20 calls or more in a period of 5 minutes the capacity is exceeded, and there will be an unwanted waiting time, hence there is a capacity of 19 calls per 5 minutes.

### a)
> What is the probability that the capacity is exceeded in a random period of 5 minutes?

$$
\lambda^{5min}=\frac{\lambda^{60min}}{12}=\frac{180}{12}= 15 \\
P(X\geqslant20) = 1 - P(X<19) = 1 - 0.8752188 = 0.1247812
$$

```R
> 1 - ppois(19, 15)
[1] 0.1247812
```

### b)

> If the probability should be at least 99% that all calls will be handled without waiting time for a randomly selected period of 5 minutes, how large should the capacity per 5 minutes then at least be?

The 0.99 quantile of the number of calls is at 25, so 99% of all randomly selected periods of 5 minutes will have at maximum 25 calls, so therefore the capacity should be 25 calls per 5 minutes.

$$
q_{0.99} = 25 
$$

```R
> qpois(0.99,15)
[1] 25
```