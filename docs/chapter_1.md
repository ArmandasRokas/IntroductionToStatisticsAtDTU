### Exercise 1.1 Infant birth weight

#### a) Females

- **sample mean** - show average including outliers  


$$
\bar{x} = \frac{2474+2547+2830+3219+3429+3448+3677+3872+4001+4116}{10} = 3361.3
$$

- **variance** - it’s the average of the distance of values from the mean squared

$$
s^2 = \frac{((2474-3361.3)^2+(2547-3361.3)^2+ 
                      (2830-3361.3)^2+\\(3219-3361.3)^2+
                      (3429-3361.3)^2+(3448-3361.3)^2+\\
                      (3677-3361.3)^2+(3872-3361.3)^2+
                      (4001-3361.3)^2+(4116-3361.3)^2}{9} = 344920.5
$$

- **standard deviation** - it's the square root of the variance. 

$$
s = \sqrt{283158.2} = 587.2993
$$



#### b) Males:

- **sample mean**


$$
\bar{x} = \frac{2844+2863+ 2963+3239+ 3379+ 3449+ 3582+ 3926+ 4151+ 4356}{10} = 3475.2
$$

- **variance** 

$$
s^2 = \frac{(2844-3475.2)^2+(2863-3475.2)^2+ (2963-3475.2)^2+ \\
                    (3239-3475.2)^2+ (3379-3475.2)^2+ (3449-3475.2)^2+\\
                    (3582-3475.2)^2+ (3926-3475.2)^2+ (4151-3475.2)^2+ 
                    (4356-3475.2)^2}{9} =  532.1261
$$

- **standard deviation**  

$$
s = \sqrt{1625049} = 532.1261
$$

- Compared with females males infant is heavier with 113.9 in average. Moreover males weight varies 55.1732‬ grams less than females. 

#### c) The five quartiles

- Females

$$
Q_{0} = q_{0} = x_{1} = 2474\\
Q_{1} = q_{0.25}= x_{25*\frac{10}{100} = x_{\lceil{2.5}\rceil}} = x_{3} = 2830 \\
Q_{2} = q_{0.50}= \frac{x_{5}+ x_{6}}{2} = \frac{3429+3448}{2} = 3438.5  \\
Q_{3} = q_{0.75} = x_{75*\frac{10}{100}} = x_{{\lceil{7.5}\rceil}} = x_{8} = 3872 \\
Q_{4} = q_{1} = x_{10} = 4116\\
$$



- Males


$$
Q_{0} = q_{0} = x_{1} = 2844\\
Q_{1} = q_{0.25}= x_{25*\frac{10}{100}} = x_{\lceil{2.5}\rceil} = x_{3} = 2963 \\
Q_{2} = q_{0.50}= \frac{x_{5}+ x_{6}}{2} = \frac{3379+3449}{2} = 3414.5  \\
Q_{3} = q_{0.75} = x_{75*\frac{10}{100}} = x_{{\lceil{7.5}\rceil}} = x_{8} = 3926 \\
Q_{4} = q_{1} = x_{10} = 4356\\
$$

- Boxplot:

  ![infant_birth_weight](pics/infant_birth_weight.png)
  
#### d) Inter Quartile Range(IQR)

$$
  IQR = q_{0.75} - q_{0.25} = Q_{3}-Q_{1}
$$

- Females 

$$
IQR = q_{0.75}- q_{0.25} = 3872 - 2830 = 1042 \\
\text{extremes} < Q_{1} - 1042 * 1.5 = 2963 - 1563 = 1400 \\
\text{OR} \\
\text{extremes} > Q_{3} + 1042 * 1.5 = 3872 + 1563 = 5435
$$

 There are no observations lower than 1400 or higher than 5435, so there are no  "extreme" observations

- Males 

$$
IQR = q_{0.75}- q_{0.25} =3926 - 2963  = 963 \\
\text{extremes} < Q_{1} - 963  * 1.5 = 2963 - 1444.5= 1518.5 \\
\text{OR} \\
\text{extremes} > Q_{3} + * 1.5 = 3926 + 1444.5  = 5370.5
$$

 There are no observations lower than 1518.5 or higher than 5370.5 , so there are no  "extreme" observations. 



#### e) The coefficient of variations

$$
V = \frac{s}{\bar{x}}
$$

- Females 
$$
V = \frac{587.2993}{3361.1}= 0.1747
$$

- Males

$$
V = \frac{532.1261}{3475.2} = 0.153121
$$

### Exercise 1.2 Course grades
#### a) Median
4
#### b) Quartiles and IQR

$$
Q_{0} = q_{0} = x_{1} = -3\\
Q_{1} = q_{0.25}= x_{25*\frac{251}{100} = x_{\lceil{62.75}\rceil}} = x_{63} = 0 \\
Q_{2} = q_{0.50}= \frac{x_{125}+ x_{126}}{2} = \frac{4+4}{2} = 4  \\
Q_{3} = q_{0.75} = x_{75*\frac{251}{100}} = x_{{\lceil{188.25}\rceil}} = x_{189} = 7 \\
Q_{4} = q_{1} = x_{10} = 12\\ 
IQR = q_{0.75}- q_{0.25} = 7 - 0  = 7  \\
$$

#### Exercise 1.3 Cholesterol

#### a) Medians

$$
\bar{b} = 8.5 \\
\bar{a} = 7.2
$$

#### b) Standard deviation
$$
s_{b} = 0.9023778 \\
s_{a} = 1.090129
$$

#### c) Sample covariance

$$
s_{ab} = \frac{1}{n-1}\sum_{i=1}^{n}{(b_{i}-\bar{b})(a_{i}-\bar{a})} = 0.7964286
$$



#### d) Correlation

$$
r = \frac{s_{ba}}{s_{b}*s_{a}} = 0.8096188
$$







#### e)

I would answer something like this: the most patients decreased cholesterol level between 1.1 and 1.6, which is Inner Quartile Range (IQR). However the worst result recorded is -0.2 and the best is 2.1.  Lastly the mean is 1.21 and the median is 1.3. 

















