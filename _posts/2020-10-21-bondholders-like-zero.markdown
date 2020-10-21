---
layout: post
title:  "Bondholders Should Like Zero Interest"
date:   2020-10-21 16:25:47 -0600
categories: mmt bonds
---

In this post, I will explain why bond holders are better off when bonds pay no interest.
We will evaluate the "real world" effects of two scenarios:
one in which bonds pay zero interest, and one in which 
bonds pay 2% interest.
For the sake of analysis, we will assume zero inflation, and that
the largest sustainable increase in U.S. debt over the next 30 years,
is $100 trillion dollars.

*__To distinguish between normal fiscal spending and interest costs,
will call normal fiscal spending "primary spending", while the
interest paid will be called "interest expense".__*


The first scenario is very easy to compute, because you simply divide
the total increase in debt, but the number of years, to get
the annual deficit.  (defined as the deficit minus interest expense).

### Scenario 1

    Initial Debt:             $27 trillion (current)
    Final Debt:              $127 trillion
    Debt Increase:           $100 trillion 
    Bond Interest Rate:         0% APR
    Time Elapsed:              30 Years
    --------------------------------------------
    Annual Primary Deficit: $3.33 trillion (no interest)
    Primary Spending:         100 trillion 
    Interest Expense:           0 trillion

The next scenario is a bit more difficult to compute,
because it is not immediately clear how much the U.S. can spend
each year, and still keep the total increase in debt below
$100 trillion.

### Scenario 2

    Initial Debt:           $27 trillion (current)
    Final Debt:            $127 trillion
    Debt Increase:         $100 trillion 
    Bond Interest Rate:       2% APR
    Years:                   30
    --------------------------------------------
    Annual Primary Deficit:  ?? trillion (excludes interest)
    Primary Spending:        ?? trillion
    Interest Expense:        ?? trillion
   
While a closed formula is possible, we will simply use an iterative
"guess and check" method, where we try different annual deficit levels
and check if the final debt level is above or below $127 trillion.

To perform this computation I wrote the following python script:

~~~python
    # All computations in trillions of USD nominal.
    principle = 27
    rate = 1.02
    end_debt = 127
    years = 30

    # 1.02^30 * principle + sum(1.02^i * deficit, i = 1 to 30)
    def compute_debt(principle, rate, deficit, years):
        return principle * rate**years + sum([
            deficit * rate ** i for i in range(years)])

    # use bisection method to find the allowed deficit level
    high = 2000
    low = 0
    epsilon = 0.01
    while abs(high-low) > epsilon:
        guess = (high + low)/2
        result = compute_debt(principle, rate, guess, years)
        if result > end_debt:
            high = guess
        else:
            low = guess
    deficit = guess
    print("principle=%s, rate=%s, end_debt=%s, years=%s" %
        (principle, rate, end_debt, years))
    print("Deficit:", deficit)
~~~
    
    
This code gives the following output:

    principle=27, rate=1.02, end_debt=127, years=30
    Deficit: 1.93023681640625

So with a 2% interest rate, the U.S. could only enjoy a $1.93 trillion dollar deficit, if it wanted to keep
its total debt below $127 trillion.

    $1.93 trillion * 30 = $57.9 trillion

This means that the U.S. would only be able 
to spend $58 trillion on primary spending and the other $42 trillion of 
the $100 trillion debt increase would
be interest expense.  Even though 2% does not sound like a very high interest
rate, it 'ads' up quickly.


We can now give the computed results for scenario 2.

### Scenario 2

    Initial Debt:             $27 trillion (current)
    Final Debt:              $127 trillion
    Debt Increase:           $100 trillion 
    Bond Interest Rate:         2% APR
    Time Elapsed:              30 Years
    --------------------------------------------
    Annual Primary Deficit: $1.93 trillion
    Primary Spending:         $58 trillion
    Interest Expense:         $42 trillion
 
Thus, the amount of primary spending possible, is in fact 42% lower over a 30 year period, if bonds pay a mere 2% in interest.

We will assume that in either scenario, bonds have the same distribution among the population,
based on their relative preference and ability to save money.  This may sound unusual,
as we are essentially saying that only the total amount of bonds changes who holds them,
and that the rate of interest has zero bearing on who holds bonds. 

So the only question then becomes:

>  Will U.S. bond holders actually be better off, if, over the next 30 years,
>  that $42 trillion goes to interest expense instead of real output?

The way we can understand this, is that bond holders will work/output
more when they are not offered interest, versus when they are offered interest, in order to meet their
desired level of savings.  So in the first scenario, bond holders are forced to generate
more output to reach that level of savings, while in the second scenario, they output a much smaller amount,
and are able to secure a large portion of their savings through interest alone.

This has limited effectiveness, because, past a certain point, the incentive 
to earn money will be less if its present value is sufficiently diminished.
Nevertheless, most earners are thinking about smaller time horizons, like 5
to 10 years, and not 30 years, so the interest difference does not make
a big difference in incentives over that time period.

Think of all the bridges that could be built, all the schools that could be upgraded,
all the science that could be done, if that $42 trillion dollars goes towards real
productive activities instead of just interest.

There is no free lunch, not even interest.
