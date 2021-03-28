---
description: >-
  We take a look at what CAGR is, how it works, and how we can compute CAGR of
  various listed assets
---

# CAGR : Point-to-point Annualized Returns

## Intro <a id="Intro"></a>

So far, we’ve covered various computations, which mostly involved algebraic sum / multiplication / subtraction.

Except, these aren't enough.

We need to add new tools in our arsenal to fully unlock the powers of excel, to aid with our day-to-day financial decision-making process.

Learning about CAGR is only the first step towards that.

## CAGR <a id="CAGR"></a>

CAGR \(**C**ompound **A**nnual **G**rowth **R**ate\) is a measure of how _fast_ a value has been growing, assuming this value is probably a result of a compounding process.

Let's assume value at the beginning of a time period was $$V_{initial}$$, and if it changed to $$V_{final}$$ over a period of time $$t$$, then CAGR or the rate of this growth, can be formulated as:

$$V_{final} = V_{initial}(1 + r/100)^t$$

Where, $$r$$ is the **annualized rate of growth** or CAGR.

This is well known formula of compounding, from your school days!

Rearranging this equation for $$r$$, we get

$$r = 100((\frac{V_{final}}{V_{initial}})^{1/t} - 1)$$

{% hint style="info" %}
In the above formula, $$r$$is greater than 1. Is we want value of $$r$$ to be within 0 and 1 \(and not 0 and 100\), we can remove multiplication by 100 from the formula. Either is fine.
{% endhint %}

To build a mental model of what this formula means, in below diagram, we plot value against time

![Compounded Growth and CAGR - Dark Mode](../../.gitbook/assets/compounded-growth.dark.png)

![Compounded Growth and CAGR - Light Mode](../../.gitbook/assets/compounded-growth.light.png)

Value can be price of an asset, based on our context and use-case.

Notice that the growth doesn’t have to _look like_ compounded growth. It's the other way around - we can _model_ it or _think of it_ as compounded growth.

This mathematical formula, just needs two values:

* $$V_{final}$$
* $$V_{initial}$$

And on top of that, time it took to go from $$V_{initial}$$ to $$V_{final}$$

In fact, either of these two points in the Y-axis could be smaller / bigger than one another, or even be negative.

**The mathematical formula above poses no restrictions on that front**.

However, in the above graph, we’ve no way of visualizing or placing $$r$$, the rate of growth \(CAGR\).

It’s a power-law formula.

Instead of plotting value vs time, we can plot **logarithm of value** against time.

{% hint style="info" %}
Discussing logarithm in detail, is out of scope for our wiki. However, if you'd like to brush up on basic logarithms, we highly recommend checking out this [YouTube video by 3Blue1Brown](https://www.youtube.com/watch?v=cEvgcoyZvB4)
{% endhint %}

Let's go back to original formula

$$V_{final} = V_{initial}(1 + \frac{r}{100})^t$$

We can take $$\log$$ of both sides of the equation, **only if both sides are positive numbers**.

{% hint style="danger" %}
Logarithm, or $$\log$$ for short, cannot be used on negative numbers - it results in _complex numbers_, which we don't want to deal with in context of investments and finance.
{% endhint %}

In the above equation, taking $$\log$$ on both sides, we get

$$
\log(V_{final}) = \log(V_{initial}(1 + \frac{r}{100})^t)
$$

We can apply formula of logarithms \(left to reader as an exercise, we won't show detail computation for that here\), to finally arrive at this:

$$
t \log{(1 + \frac{r}{100})}  = [\log {V_{final}} - \log {V_{initial}}]
$$

This is effectively the straight line equation, similar to $$y = mx + c$$. In this scenario, $$t$$is effectively the X-axis, while Y-axis is $$\log{V}$$.

We can now update our diagram's Y-axis

![Logarithm of value vs time - Dark Mode](../../.gitbook/assets/log-compounded-growth.dark.png)

![Logarithm of value vs time - Light Mode](../../.gitbook/assets/log-compounded-growth.light.png)

We have plotted $$\log$$ of values \(Y-axis\) versus time \(X-axis\). Then we've joined the start point and end point with a dotted straight-line.

The slope of a straight line joining those two points $$A$$ and $$B$$, is $$\log{(1 + \frac{r}{100})}$$, and can be used to compute $$r$$.

## 3Y Return CAGR

A common use of CAGR is to compute returns of a mutual fund or a stock portfolio watchlist \(e.g. Smallcase\).

Let's begin with a common one: 3 year \(often written as **3Y**, for short\) return of a mutual fund.

Most mutual fund platforms report annualized returns for time periods greater than 1 year, while absolute percentage growth for time periods smaller than 1 year.

It's an accepted norm.

At exact 1 year mark, either can be reported, since both would be same \(annualized and absolute _return_\).  
  
Returns above 1 year, are reported as _annualized rate of growth_, often appended with _per annum_ \(**p.a.**, for short\).

We know that index funds track the index. In rest of this chapter, we'd compute and compare CAGR of Nifty, and that of a Nifty index fund over an arbitrary period of time.

From Valueresearch Online, [UTI Nifty Index Fund Direct Growth](https://www.valueresearchonline.com/funds/15830/uti-nifty-index-fund-direct-plan) \([archive.org link](https://web.archive.org/web/20210122010723/https://www.valueresearchonline.com/funds/15830/uti-nifty-index-fund-direct-plan) \| [archive.is link](https://archive.is/zSHxj)\) has 3Y return of **13.72% p.a.**, as on **26th Mar 2021**. Exact date is important, since this 3Y return value would change with date.

![VRO UTI Nifty Index Direct Growth Returns Table - Dark Mode](../../.gitbook/assets/vro-uti-nifty-index-return.dark.png)

![VRO UTI Nifty Index Direct Growth Returns Table - Light Mode](../../.gitbook/assets/vro-uti-nifty-index-return.light.png)

Notice the value under **3-Y** column, noted as **13.72**.

This is effectively 3Y CAGR of the fund. It means, as on 26th March, 2021; 3 year CAGR of this fund was 13.72% p.a.

Our task would be to do these:

* validate this number, computing it ourselves
* compare against CAGR of Nifty over same time period

### Validating Fund 3Y CAGR

We need historical NAV data for this.

One way we can obtain it via Google Finance. Ticker symbol for UTI Nifty Index Direct Growth is `"MUTF_IN:UTI_NIFT_INDE_1HPGBNK"`.

Another option would be to use the AMFI endpoint for latest NAV, and ISIN of this fund to lookup the latest NAV, as we've discussed in a previous chapter.

But remember that CAGR needs only two data points. In this case, since we only need two data points, we can just manually look it up. And enter these two data point values into our excel sheet or spreadsheet manually.

Steps to follow:

* Head over to AMFI historic NAV page URL: [https://www.amfiindia.com/net-asset-value/nav-history](https://www.amfiindia.com/net-asset-value/nav-history)  This is different from other AMFI links / URLs we've seen in the past. It's a dedicated URL, where AMFI offers the user an option to select date range, fund name etc.; and receive NAV of a given fund between those two dates, both inclusive. 
* Search for dates around 26th March, 2021 \(select two dates, that are less than 90 days apart, and covers the given date\); we find the latest NAV as **96.7892** for UTI Nifty Index Direct Growth.  You could, for instance, select 1st March 2021 as one date, and 31st March 2021 as second date. These two dates are less than 90 days apart, and has the given date in its range. 
* Enter these info in a freshly created spreadsheet as follows:

  | Date | NAV |
  | :--- | :--- |
  | 26/03/2018 | 65.7954 |
  | 26/03/2021 | 96.7892 |

* Spreadsheet doesn't have an in-built `CAGR()` function, but we can make do with `RRI()` function for now \(we'd see better options in a later chapter\).  [Documentation for RRI function](https://support.google.com/docs/answer/9368238?hl=en) \| [archive.org link](https://web.archive.org/web/20200807053259/https://support.google.com/docs/answer/9368238?hl=en) \| [archive.is link](https://archive.is/u3SsD)  Invoke it as  `RRI(   3,   <cellID for value from 3 years ago>,    <cellID for value as on today> )`

![CAGR 3Y Computed with RRI\(\) - Dark Mode](../../.gitbook/assets/cagr-3-year.dark.png)

![CAGR 3Y Computed with RRI\(\) - Light Mode](../../.gitbook/assets/cagr-3-year.light.png)

But instead of using the `RRI()` function, we could directly use the mathematical formula as we'd discussed above: $$V_{final}$$being the value on given date, $$V_{initial}$$ is the value on given date 3 years ago; and $$t$$ is 3, for 3 years.

We'd get this

![CAGR of 3 Years Computed - Dark Mode](../../.gitbook/assets/cagr-3y-computed.dark.png)

![CAGR of 3 Years Computed - Light Mode](../../.gitbook/assets/cagr-3y-computed.light.png)

Notice that we've used 0.33 for $$1/t$$, to denote $$t = 3$$. This is **not** correct. We could get more accurate estimation, directly using $$1/3$$ instead of using 0.33.

However, the number of days between any two arbitrary dates cannot always be expressed as whole number of years. It might have leap-years, for example.

We see that computed value of **13.58%** is quite close to **13.72%** as reported, but we are not quite there yet.

On the other hand, growth rate computed using in-built formula is close to the reported value of 3Y return on Valueresarch Online portal.

{% hint style="info" %}
 Based on today's date, you might get a different value of latest NAV. You should use 3Y return as on today, and search for NAV as on dates near today's date, or dates from 3 years ago.
{% endhint %}

{% hint style="warning" %}
At the time of writing this, AMFI historic NAV provides NAV data on a maximum of 90 day period, at once. If you're searching for NAV for a particular date, adjust the start date and end date in a way, that would select any 90 day or smaller duration window, which covers that particular date.
{% endhint %}

We've used `GOOGLEFINANCE()` to prepare this video for guidance

{% embed url="https://www.youtube.com/watch?v=F2cLCI\_Nwn0" caption="Calculation of CAGR for Mutual Fund using Google Finance - Dark Mode" %}

{% embed url="https://www.youtube.com/watch?v=EvugA04SAe8" caption="Calculation of CAGR for Mutual Fund using Google Finance - Light Mode" %}

### Cross-checking Nifty 3Y CAGR

Now that we've verified CAGR of the index fund over 3 years, independently, and matched with reported CAGR on an aggregator portal; it's time to compare with Nifty CAGR over same period.

Once again, we can use `GOOGLEFINANCE()` for getting historic Nifty price data. The ticker for Nifty can be `"NIFTY_50"` or `"INDEXNSE:NIFTY_50"`.

{% embed url="https://www.youtube.com/watch?v=3LD3Pesl0eY" caption="Computing CAGR of Nifty with Google Finance - Dark Mode" %}

{% embed url="https://www.youtube.com/watch?v=2xbL4UwQ9og" caption="Computing CAGR of Nifty with Google Finance - Light Mode" %}

Final results as it can be

![Nifty 3Y CAGR vs UTI Nifty Index Direct Growth 3Y CAGR - Dark Mode](../../.gitbook/assets/nifty-cagr-vs-uti-nifty-cagr-3y.dark.png)

![Nifty 3Y CAGR vs UTI Nifty Index Direct Growth 3Y CAGR - Light Mode](../../.gitbook/assets/nifty-cagr-vs-uti-nifty-cagr-3y.light.png)

As you can see from this computation, or above image\(s\); the CAGR numbers of UTI Nifty Index Fund - Direct Growth, and CAGR numbers for Nifty itself; **do not match**.

In fact, this has nothing to do with the dates. You could select a different set of dates, 3 year apart; and the return from Nifty Index fund would be slightly higher than Nifty 3Y CAGR.

In this case, 3Y CAGR as on 26th March 2021 is 13.73% p.a. for UTI Nifty Index Direct Growth. While, for Nifty itself, it’s slightly lower, 12.52% p.a.

This is expected!

An index fund tracks the TRI \(**T**otal **R**eturn **I**ndex\), and not the vanilla price index.

TRI is price index + dividends.

Therefore, over any given period of time

* Nifty index funds can have slightly higher return than Nifty itself.
* If no dividends were announced in that time period, it can be expected that Nifty index fund CAGR are close to that of Nifty CAGR itself.
* As time periods get longer \(10Y / 15Y / 20Y\), this difference becomes more and more stark between CAGR of Nifty and a Nifty index fund.

These have nothing special to do with Nifty itself. If you’d instead picked an S&P500 index fund, or a NASDAQ index fund - similar observations would’ve held true.

We can satisfy our curiosity, by comparing against Nifty Total Return Index CAGR.

### Nifty Total Return Index 3Y CAGR

Similar to last two computations, we just have to switch the ticker.

Except, to the best of our knowledge, Google Finance has **no ticker for Nifty Total Return Index**.

In other words, we’ve to manually find and enter these values in our sheet, to compute CAGR.

We can obtain these from official NSE India website for historic data on total return index: [https://www1.nseindia.com/products/content/equities/indices/historical\_total\_return.htm](https://www1.nseindia.com/products/content/equities/indices/historical_total_return.htm)

Plugging in values for the two dates manually, and computing as earlier, we get this

![Nifty TRI 3Y CAGR - Dark Mode](../../.gitbook/assets/nifty-tri-3y-cagr.dark.png)

![Nifty TRI 3Y CAGR - Light Mode](../../.gitbook/assets/nifty-tri-3y-cagr.light.png)

3Y CAGR of Nifty TRI, as on 26th March 2021, stands at **14.09% p.a.**

This is much closer to the CAGR of UTI Nifty Index - Direct Growth.

However, the CAGR is slightly higher.

An index fund is _supposed to_ mimic the total return index, but there can be inefficiencies. Hence, CAGR over a given period can be somewhat different in practice, with some _**tracking error**_.

We won’t discuss tracking error in detail here. But we’d emphasize tracking error can be both positive and negative in value.

In other words, due to inefficiencies in tracking the index, the CAGR of the index fund can be both higher or lower than CAGR of the total return index, over any given period.

## Visualization

We had mentioned earlier how CAGR relates to slope of a straight line joining two points, in a log-plot of asset prices.

We shall now plot these price points in a graph where price values are logarithmic, and try to validate that our visual idea about CAGR holds true.

{% hint style="info" %}
Since the Y-axis is in log scale, but X-axis is in normal scale; such plots are called _semi-log plots_. For it to be a log plot, both X and Y axes have to be in log scale.
{% endhint %}

Spreadsheets have fantastic charting / plotting abilities built in. You could use the Charting button on toolbar, or just select an area of cells which has data, then use `Insert` →`Chart`

Refer to this video on how to get this working

{% embed url="https://www.youtube.com/watch?v=JXSn2dZ0Qek" caption="Semi-log Plot for CAGR Visualization - Dark Mode" %}

{% embed url="https://www.youtube.com/watch?v=eEAseRxyaAk" caption="Semi-log Plot for CAGR Visualization - Light Mode" %}

![Semi-log plot of all datasets - Dark Mode](../../.gitbook/assets/nifty-3y-cagr-semilog-plot.dark.png)

![Semi-log plot of all datasets - Light Mode](../../.gitbook/assets/nifty-3y-cagr-semilog-plot.light.png)

We see from the videos / images above, that once we switch the Y-axis to logarithmic values, the three lines start to look parallel to each other.

Parallel lines have same slope, and since slope of these lines relate to CAGR of the underlying data set, through a logarithmic relationship; it stands to reason that these would seem parallel to the naked eye.

Notice that right up until the moment we converted Y-axis values to logarithmic scale, the line for UTI Nifty Index fund was nearly flatlining, kissing the X-axis closely.

This was because compared to absolute values of Nifty or Nifty TRI, which are above 10k in this dataset; NAV of this fund was barely even 100. It’d practically be dwarfed in a vanilla line graph.

However, once we switched to semi-log mode, all three lines started reflecting real growth over time in their _tilt_ \(or slope\).

It should intuitively make it clear that absolute value of an underlying asset's price value is immaterial when you purchase it, or the range of absolute values it moves between; only thing that matters is the growth rate _after_ you purchase the asset.

An asset whose price moves between 10 and 20, is not that different from an asset whose price moves between 10,000 and 20,000.

The downside of such visualization is unless the difference is stark, or a larger time periods are chosen; most such semi-log plots would result in near-parallel lines in a line graph.

## Recap and Wrapping Up

When it comes to spreadsheet / excel functionalities, in this chapter, we learned

* how to draw semi-log plots
*  how to use `RRI()`

We have also gained new insights into a demystified process of _return calculation_.

Next time we see CAGR reported on any portal such as MoneyControl, Valueresearch Online, Morningstar, CRISIL, BSE India, Kuvera, Coin, PayTM Money, INDMoney, Piggy, ETMoney, or even Smallcase etc.; we’d know how to compute and validate these numbers ourselves.  
  
These platforms and portals are computing these numbers from historic NAV data they have obtained; and now we can compute the same as well.

#### A word of caution <a id="A-word-of-caution"></a>

CAGR is a point-to-point metric. Given any two points in a plane, a straight line can always be drawn to connect those two points. This is one of the fundamental axioms of geometry, known as one of the core axiom of _Axioms of Euclidean Plane Geometry._

It says nothing about the _journey_ or price-movement in-between.

For instance, the computation above might have painted a rosy picture, that one might falsely assume _Nifty can easily achieve 12.5%-14% p.a. return over a 3 year time period_.

**This is wrong, and dangerous to assume**.

The actual journey of Nifty 50 index between those two dates, can be viewed as this \(plotted using real Nifty price data, which can be obtained from Google Finance\). This is also a semi-log plot, where the price axis \(Y-axis\) is consisted of log values.

![Nifty actual price movement 3Y period - Dark Mode](../../.gitbook/assets/nifty-price-3y-movement.dark.png)

![Nifty actual price movement 3Y period - Light Mode](../../.gitbook/assets/nifty-price-3y-movement.light.png)

As Nifty TRI and Nifty index fund move closely with Nifty 50 itself; plotting these would lead to similar looking graphs, with lot of volatility.

What we’re doing when we compute CAGR, is to connect the starting point and last point on the graph with a straight line, then compute slope of that line.

Since two points on a plane can be connected with so many different lines and line segments \(can be curves\); there are infinite possibilities of the _journey within that time period_, which CAGR computation won’t capture.

We’ve alluded to this in one of our previous chapters, where we had computed NASDAQ-based portfolio’s final value. And we’ve shown that NASDAQ’s point-to-point return of near zero, didn’t show up exactly as that in a DCA / SIP portfolio in NASDAQ.

Similarly, CAGR alone cannot produce any information, on the price movement of an asset within a time period.

In next chapter, we’d be introduced to a more generalized measure, that captures more relevant information.
