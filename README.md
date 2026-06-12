# NPL-Portfolio-Pricer
NPL portfolio pricer with Monte Carlo simulation, stress testing, and correlated systemic shock model.

## What it does
We first set the parameters with assumptions on times to foreclosure, haircuts on value for REOs and auctions, legal costs, loss mitigation 
probabilities, etc, in order to predict what a probabilistic outcome for a specific loan would be. Each loan follows a decision tree based on the US foreclosure framework — loss mitigation, foreclosure through judicial or non-judicial track (determined by state), auction, and REO. All cash flows are discounted at the investor's required return.

Afterwards, we run a Monte Carlo simulation to price the full portfolio across 10,000 different simulations. We also build a correlated version that adds a systemic market shock to all property values simultaneously — this nearly doubles portfolio volatility without changing the expected value, showing that correlation increases tail risk, not expected return.

Finally, we run three sensitivity analyses to stress test the portfolio under different assumptions.

## Risk metrics
**Systemic shock** — a single market-wide draw that shifts all property values simultaneously, creating correlation across loans

**Tail risk** — measured as the 5th percentile of the portfolio price distribution; the correlated model shows significantly worse tail risk than the independent model

## Sensitivity analyses
- Property value shocks (-40% to +20%)
- Required return (10% to 15%)
- Foreclosure timeline (0.75x to 2.00x base case)

## Parameters
- d: Investor required return
- p_loss_mitigation: Probability of pre-foreclosure resolution
- p_sell_auction: Probability of third-party auction purchase
- p_occupied: Probability of occupied REO
- h_auction: Auction haircut on property value
- h_REO: REO haircut on property value
- sigma: Market shock volatility (correlated model)

## Libraries
numpy, pandas, matplotlib

## Output
The total price an investor asking for a required return of 12% would pay is $5,973,007.04.
Paying 50.31 cents on the dollar.

Different Return Portfolio Price   vs Base
             10%      $6,153,817  $187,582
             11%      $6,045,133   $78,898
             12%      $5,966,235        $0
             13%      $5,904,787  $-61,447
             14%      $5,805,791 $-160,444
             15%      $5,756,822 $-209,413
             
Different foreclosure time Portfolio Price   vs Base
                     0.75x      $6,207,287  $235,120
                     1.00x      $5,972,167        $0
                     1.25x      $5,772,668 $-199,499
                     1.50x      $5,516,373 $-455,795
                     1.75x      $5,342,922 $-629,245
                     2.00x      $5,142,623 $-829,544


Price Shock Portfolio Price     vs Base
       -40%      $3,594,462 $-2,374,336
       -30%      $4,183,634 $-1,785,163
       -20%      $4,764,642 $-1,204,155
       -10%      $5,382,684   $-586,113
         0%      $5,968,797          $0
        10%      $6,575,421    $606,623
        20%      $7,150,477  $1,181,680
        
Comparison between simple Monte Carlo and with systemic shock:
Base mean: $5,968,999
Correlated mean: $5,969,706
Base std: $368,922
Correlated std: $703,194
Base 5th percentile: $5,428,884
Correlated 5th percentile: $4,844,537
