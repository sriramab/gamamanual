# Extension ummisco.gaml.extensions.stats

## Table of Contents
### Operators
[auto_correlation](#auto_correlation), [beta](#beta), [binomial_coeff](#binomial_coeff), [binomial_complemented](#binomial_complemented), [binomial_sum](#binomial_sum), [chi_square](#chi_square), [chi_square_complemented](#chi_square_complemented), [correlation](#correlation), [covariance](#covariance), [dnorm](#dnorm), [durbin_watson](#durbin_watson), [gamma](#gamma), [gamma_distribution](#gamma_distribution), [gamma_distribution_complemented](#gamma_distribution_complemented), [incomplete_beta](#incomplete_beta), [incomplete_gamma](#incomplete_gamma), [incomplete_gamma_complement](#incomplete_gamma_complement), [kurtosis](#kurtosis), [lgamma](#lgamma), [log_gamma](#log_gamma), [moment](#moment), [normal_area](#normal_area), [normal_density](#normal_density), [normal_inverse](#normal_inverse), [pbinom](#pbinom), [pchisq](#pchisq), [percentile](#percentile), [pgamma](#pgamma), [pnorm](#pnorm), [pValue_for_fStat](#pValue_for_fStat), [pValue_for_tStat](#pValue_for_tStat), [quantile](#quantile), [quantile_inverse](#quantile_inverse), [rank_interpolated](#rank_interpolated), [rms](#rms), [skew](#skew), [student_area](#student_area), [student_t_inverse](#student_t_inverse), [variance](#variance), 

### Statements


### Skills


### Architectures



### Species



----

## Operators
	
----

### `auto_correlation`
* **Possible use:** 
  * container OP int --->  float 
* **Result:** Returns the auto-correlation of a data sequence

[Top of the page](#table-of-contents)
  	
----

### `beta`
* **Possible use:** 
  * float OP float --->  float 
* **Result:** Returns the beta function with arguments a, b.

[Top of the page](#table-of-contents)
  	
----

### `binomial_coeff`
* **Possible use:** 
  * int OP int --->  float 
* **Result:** Returns n choose k as a double. Note the integerization of the double return value.

[Top of the page](#table-of-contents)
  	
----

### `binomial_complemented`
* **Possible use:** 
  * OP(int, int, float) --->  float 
* **Result:** Returns the sum of the terms k+1 through n of the Binomial probability density, where n is the number of trials and P is the probability of success in the range 0 to 1.

[Top of the page](#table-of-contents)
  	
----

### `binomial_sum`
* **Possible use:** 
  * OP(int, int, float) --->  float 
* **Result:** Returns the sum of the terms 0 through k of the Binomial probability density, where n is the number of trials and p is the probability of success in the range 0 to 1.

[Top of the page](#table-of-contents)
  	
----

### `chi_square`
* **Possible use:** 
  * float OP float --->  float 
* **Result:** Returns the area under the left hand tail (from 0 to x) of the Chi square probability density function with df degrees of freedom.

[Top of the page](#table-of-contents)
  	
----

### `chi_square_complemented`
* **Possible use:** 
  * float OP float --->  float 
* **Result:** Returns the area under the right hand tail (from x to infinity) of the Chi square probability density function with df degrees of freedom.

[Top of the page](#table-of-contents)
  	
----

### `correlation`
* **Possible use:** 
  * container OP container --->  float 
* **Result:** Returns the correlation of two data sequences

[Top of the page](#table-of-contents)
  	
----

### `covariance`
* **Possible use:** 
  * container OP container --->  float 
* **Result:** Returns the covariance of two data sequences

[Top of the page](#table-of-contents)
  	
----

### `dnorm`
Same signification as [normal_density](#normal_density)

[Top of the page](#table-of-contents)
  	
----

### `durbin_watson`
* **Possible use:** 
  * OP(container) --->  float 
* **Result:** Durbin-Watson computation

[Top of the page](#table-of-contents)
  	
----

### `gamma`
* **Possible use:** 
  * OP(float) --->  float 
* **Result:** Returns the value of the Gamma function at x.

[Top of the page](#table-of-contents)
  	
----

### `gamma_distribution`
* **Possible use:** 
  * OP(float, float, float) --->  float 
* **Result:** Returns the integral from zero to x of the gamma probability density function.  
* **Comment:** incomplete_gamma(a,x) is equal to pgamma(a,1,x).

[Top of the page](#table-of-contents)
  	
----

### `gamma_distribution_complemented`
* **Possible use:** 
  * OP(float, float, float) --->  float 
* **Result:** Returns the integral from x to infinity of the gamma probability density function.

[Top of the page](#table-of-contents)
  	
----

### `incomplete_beta`
* **Possible use:** 
  * OP(float, float, float) --->  float 
* **Result:** Returns the regularized integral of the beta function with arguments a and b, from zero to x.

[Top of the page](#table-of-contents)
  	
----

### `incomplete_gamma`
* **Possible use:** 
  * float OP float --->  float 
* **Result:**  Returns the regularized integral of the Gamma function with argument a to the integration end point x.

[Top of the page](#table-of-contents)
  	
----

### `incomplete_gamma_complement`
* **Possible use:** 
  * float OP float --->  float 
* **Result:** Returns the complemented regularized incomplete Gamma function of the argument a and integration start point x.

[Top of the page](#table-of-contents)
  	
----

### `kurtosis`
* **Possible use:** 
  * OP(container) --->  float
  * float OP float --->  float 
* **Result:** Returns the kurtosis (aka excess) of a data sequenceReturns the kurtosis (aka excess) of a data sequence

[Top of the page](#table-of-contents)
  	
----

### `lgamma`
Same signification as [log_gamma](#log_gamma)

[Top of the page](#table-of-contents)
  	
----

### `log_gamma`
* **Possible use:** 
  * OP(float) --->  float 
* **Result:** Returns the log of the value of the Gamma function at x.

[Top of the page](#table-of-contents)
  	
----

### `moment`
* **Possible use:** 
  * OP(container, int, float) --->  float 
* **Result:** Returns the moment of k-th order with constant c of a data sequence

[Top of the page](#table-of-contents)
  	
----

### `normal_area`
* **Possible use:** 
  * OP(float, float, float) --->  float 
* **Result:** Returns the area to the left of x in the normal distribution with the given mean and standard deviation.

[Top of the page](#table-of-contents)
  	
----

### `normal_density`
* **Possible use:** 
  * OP(float, float, float) --->  float 
* **Result:** Returns the probability of x in the normal distribution with the given mean and standard deviation.

[Top of the page](#table-of-contents)
  	
----

### `normal_inverse`
* **Possible use:** 
  * OP(float, float, float) --->  float 
* **Result:** Returns the x in the normal distribution with the given mean and standard deviation, to the left of which lies the given area. normal.Inverse returns the value in terms of standard deviations from the mean, so we need to adjust it for the given mean and standard deviation.

[Top of the page](#table-of-contents)
  	
----

### `pbinom`
Same signification as [binomial_sum](#binomial_sum)

[Top of the page](#table-of-contents)
  	
----

### `pchisq`
Same signification as [chi_square](#chi_square)

[Top of the page](#table-of-contents)
  	
----

### `percentile`
Same signification as [quantile_inverse](#quantile_inverse)

[Top of the page](#table-of-contents)
  	
----

### `pgamma`
Same signification as [gamma_distribution](#gamma_distribution)

[Top of the page](#table-of-contents)
  	
----

### `pnorm`
Same signification as [normal_area](#normal_area)

[Top of the page](#table-of-contents)
  	
----

### `pValue_for_fStat`
* **Possible use:** 
  * OP(float, int, int) --->  float 
* **Result:** Returns the P value of F statistic fstat with numerator degrees of freedom dfn and denominator degress of freedom dfd. Uses the incomplete Beta function.

[Top of the page](#table-of-contents)
  	
----

### `pValue_for_tStat`
* **Possible use:** 
  * float OP int --->  float 
* **Result:** Returns the P value of the T statistic tstat with df degrees of freedom. This is a two-tailed test so we just double the right tail which is given by studentT of -|tstat|.

[Top of the page](#table-of-contents)
  	
----

### `quantile`
* **Possible use:** 
  * container OP float --->  float 
* **Result:** Returns the phi-quantile; that is, an element elem for which holds that phi percent of data elements are less than elem. The quantile need not necessarily be contained in the data sequence, it can be a linear interpolation.

[Top of the page](#table-of-contents)
  	
----

### `quantile_inverse`
* **Possible use:** 
  * container OP float --->  float 
* **Result:** Returns how many percent of the elements contained in the receiver are <= element. Does linear interpolation if the element is not contained but lies in between two contained elements.

[Top of the page](#table-of-contents)
  	
----

### `rank_interpolated`
* **Possible use:** 
  * container OP float --->  float 
* **Result:** Returns the linearly interpolated number of elements in a list less or equal to a given element. The rank is the number of elements <= element. Ranks are of the form {0, 1, 2,..., sortedList.size()}. If no element is <= element, then the rank is zero. If the element lies in between two contained elements, then linear interpolation is used and a non integer value is returned.

[Top of the page](#table-of-contents)
  	
----

### `rms`
* **Possible use:** 
  * int OP float --->  float 
* **Result:** Returns the RMS (Root-Mean-Square) of a data sequence. The RMS of data sequence is the square-root of the mean of the squares of the elements in the data sequence. It is a measure of the average size of the elements of a data sequence.

[Top of the page](#table-of-contents)
  	
----

### `skew`
* **Possible use:** 
  * OP(container) --->  float
  * float OP float --->  float 
* **Result:** Returns the skew of a data sequence.Returns the skew of a data sequence, which is moment(data,3,mean) / standardDeviation3

[Top of the page](#table-of-contents)
  	
----

### `student_area`
* **Possible use:** 
  * float OP int --->  float 
* **Result:** Returns the area to the left of x in the Student T distribution with the given degrees of freedom.

[Top of the page](#table-of-contents)
  	
----

### `student_t_inverse`
* **Possible use:** 
  * float OP int --->  float 
* **Result:** Returns the value, t, for which the area under the Student-t probability density function (integrated from minus infinity to t) is equal to x.

[Top of the page](#table-of-contents)
  	
----

### `variance`
* **Possible use:** 
  * OP(float) --->  float
  * OP(int, float, float) --->  float 
* **Result:** Returns the variance of a data sequence. That is (sumOfSquares - mean*sum) / size with mean = sum/size.Returns the variance from a standard deviation.

[Top of the page](#table-of-contents)
  	

----

## Skills
	

----

## Statements
		
	
----

## Species
	
	
----

## Architectures 
	