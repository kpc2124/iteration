writing\_functions
================
Kristi Chau
10/24/2019

## Get started

We’re going to write some functions.

Here’s z-scores

``` r
x = rnorm(n = 30, mean = 4, sd = 2.3)
x_again = rnorm(n = 30, mean = 6, sd = .3)

(x - mean(x)) / sd(x)
```

    ##  [1] -0.767120446  0.109493425 -0.993470503  1.637039863  0.267334741
    ##  [6] -0.977065475  0.438222871  0.709719461  0.533829741 -0.419692475
    ## [11]  1.546684110  0.332624325 -0.761479160 -2.485776741  1.128069748
    ## [16] -0.137851865 -0.106748415  0.932105430  0.799422547  0.553437533
    ## [21]  0.905205442  0.757128408 -0.008541293 -2.241925304  0.581490604
    ## [26] -0.149966223 -0.257816586 -1.680744021 -0.606639531  0.363029790

``` r
(x_again - mean(x_again)) / sd(x_again)
```

    ##  [1]  1.5413954 -0.2961850  0.3204956 -0.2345965 -1.8983946 -0.6887392
    ##  [7] -0.6627062 -0.2415224  1.2161757  0.7926368 -0.3738088 -0.4855096
    ## [13]  0.7093845  0.5329776 -1.0329536 -1.0565157  0.2914637  0.7993727
    ## [19] -0.3082034  0.9409190  0.3336151 -0.9364778  0.2619634 -1.5869527
    ## [25]  1.6348722  2.3231173 -0.6286716 -1.4797904  0.5493942 -0.3367558

Now a function

``` r
z_score = function(x_arg) {
  
  if (!is.numeric(x_arg)) { 
    stop("x should be numeric")
  } else if (length(x_arg) < 3) { 
    stop("x should be longer than 3")
  }
  
  (x_arg - mean(x_arg)) / sd(x_arg)
  
}
```

Try out the
    function

``` r
z_score(x_arg = x_again) ## need to tell the function what x is equal to
```

    ##  [1]  1.5413954 -0.2961850  0.3204956 -0.2345965 -1.8983946 -0.6887392
    ##  [7] -0.6627062 -0.2415224  1.2161757  0.7926368 -0.3738088 -0.4855096
    ## [13]  0.7093845  0.5329776 -1.0329536 -1.0565157  0.2914637  0.7993727
    ## [19] -0.3082034  0.9409190  0.3336151 -0.9364778  0.2619634 -1.5869527
    ## [25]  1.6348722  2.3231173 -0.6286716 -1.4797904  0.5493942 -0.3367558

``` r
## z_score(x_arg = 3)
## z_score(x_arg = "my name is jeff")
## z_score(x_arg = c(TRUE, TRUE, FALSE, TRUE))
## z_score(x_arg = iris)
```

## Multiple outputs

``` r
mean_and_sd = function(input_x) {
  
    if (!is.numeric(input_x)) { 
    stop("x should be numeric")
  } else if (length(input_x) < 3) { 
    stop("x should be longer than 3")
  }
  
  list(
    mean_input = mean(input_x),
    sd_input = sd(input_x),
    z_score = (input_x - mean(input_x)) / sd(input_x)
  )
  
}
```

Test this function

``` r
mean_and_sd(input_x = x)
```

    ## $mean_input
    ## [1] 4.189654
    ## 
    ## $sd_input
    ## [1] 2.125478
    ## 
    ## $z_score
    ##  [1] -0.767120446  0.109493425 -0.993470503  1.637039863  0.267334741
    ##  [6] -0.977065475  0.438222871  0.709719461  0.533829741 -0.419692475
    ## [11]  1.546684110  0.332624325 -0.761479160 -2.485776741  1.128069748
    ## [16] -0.137851865 -0.106748415  0.932105430  0.799422547  0.553437533
    ## [21]  0.905205442  0.757128408 -0.008541293 -2.241925304  0.581490604
    ## [26] -0.149966223 -0.257816586 -1.680744021 -0.606639531  0.363029790

## Multiple inputs

``` r
sim_data = tibble(
  x = rnorm(30, mean = 1, sd = 1),
  y = 2 + 3 * x + rnorm(30, 0, 1)
)

ls_fit = lm(y ~ x, data = sim_data) ## fits simple linear regreession
  
beta0_hat = coef(ls_fit)[1] ## extract estimated intercept
beta1_hat = coef(ls_fit)[2] ## estimated slope
```

``` r
sim_regression = function(n, beta0, beta1) {
  
  sim_data = tibble(
    x = rnorm(n, mean = 1, sd = 1),
    y = beta0 + beta1 * x + rnorm(n, 0, 1)
    )

  ls_fit = lm(y ~ x, data = sim_data)
  
  tibble(
    beta0_hat = coef(ls_fit)[1],
    beta1_hat = coef(ls_fit)[2]
  )
  
}

sim_regression(n = 3000, beta0 = 17, beta1 = -3)
```

    ## # A tibble: 1 x 2
    ##   beta0_hat beta1_hat
    ##       <dbl>     <dbl>
    ## 1      17.0     -2.99
