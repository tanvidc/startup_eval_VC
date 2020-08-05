# Marketplace startup evaluation for investment
 
Initech is a marketplace startup. We have data of revenue per employer and worker per month, from Jan 2015 to May 2019 that include market of operation and revenue after direct costs. A preliminary look at the data shows that all workers, barring the very initial that operated in "other" market in addition to one of the cities, operate in only one city. This tells me that the marketplace is likely for a physical service: TaskRabbit-like, or on-site consultant, nurse-staffing, substitute teacher staffing (liquidity provider), etc. If Initech were similar to Upwork as stated in the prompt, work would've been location-agnostic.

## Income Statement

Disclaimer: I haven't formally learnt or worked with income statements before. So although this analysis is based on what seems logical to me, and a quick search and learn.

1. Initech has spent $14M of its $20M funding and has a 5-6 month runway with current status.

2. Worker pay is 75-90% of the revenue, with a mean of ~84%. Gross margin is -2% to 21% barring an outlier: quite volatile, and fairly low compared to some marketplaces we might've heard of (https://blog.dealroom.co/farfetch-5-6-billion-valuation-a-closer-look/). Mean, stdev, and box-plots can be found in initech.xlsx > income_stmts tab. 

Of course, Initech is early stage, so there is potential for gain with scale, but those gains will likely be in reduced indirect costs unless the worker service is low skilled. If the service is in a specialized sector like nursing where the potential labor pool is not very big, Initech will not be able to reduce %worker pay. 

3. Customer support is a major indirect cost. This is probably in the form of refunds, although it could be outsourced phone/online customer support. Worker quality control, stricter guidelines, etc. can reduce this cost.

![income_stmts](https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/inst.PNG)

4. Income statement items are plotted against time. Payment processing stands out, since it isn't correlated with revenue. The payment processing fees are usually a fixed amount and a percentage. Perhaps the transaction size change is causing this. ie when the revenue is high but payment processing cost hasn't increased, there were fewer larger transactions.

## Accounting for user growth

<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/growth.PNG" width="800">
1. Quick ratio measures how efficiently a company is growing in terms of users or revenue gained per every user or or revenue lost (this metric and others we'll discus were inspired from the awesome post by tribecap.co).
We don't see any phase lag between employer and worker growth. Hmm. Without any lag, and without transaction data, we can't definitively say the limiting factor. In many marketplaces, payer acquisition takes more effort than payee (companies like Uber are an exception, because the service provided was substantially better than status quo, and large sign up bonuses needed to be offered to create a critical size driver network). 

<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/wgrowth.PNG" width="800">
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/egrowth.PNG" width="800">
2. The elephant in the room: holiday churn. Most users are ressurected after the Thanksgiving/Christmas dip. Given time, I'd make perhaps 4-month windows (in addition to monthly here) and see retention from Oct to Feb. Since employer marketing and sales, and worker marketing are substantial costs, looking at retention barring holiday dip is worth looking at. During normal times, retention is ~77% for both workers and employers. Quick ratio ~1.3 for both as well, outside of seasonal anomalies.

## Accounting for revenue growth
Just like users, we see a dip around holidays, but most of that revenue is regained by February of the following year, but increased amounts spent on sales and marketing, and a discount campaign in 2018 might be a factor in pulling these users back.
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/emrr.PNG" width="800">
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/wmrr.PNG" width="800">
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/mrr.PNG" width="800">

## Cohort LTV
In the ~2.5 days I took to work on this take-home, I haven't been able to work on this section fully. Irrespective of the hiring decision, I plan to come back to this section when I find some time, likely the week of Aug 17 2020. 
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/e_ltv.PNG" width="600">

I decided to split the cohorts into 3-month chunks (quarterly) because visualizing 18 cohorts might work better than 54 cohorts. The plot shows that the early sign up employers continue generating higher revenue each month than the newer ones. The curves are super-linear, which means that revenue per month for each cohort is inceasing over time. That's a good sign. The heatmap below is another way to see that the initial cohorts contributed to increased revenue faster.

<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/e_ltv_hm.PNG" width="600">

## Other considerations
There are so many other factors that would affect investment decision: some qualitative, and some potentially quantitative ones that we don't have data for. For example, experience or economic advantage vs status quo, opportunity for technology to add value, current fragmentation, friction vs incentive to change, market size (both employer and worker side), and team potential. I'd ask them about transaction size, choice of markets and market performance, 

## Tid-bits
### Markets
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/city.PNG" width="800">
Most markets are minuscule compared to SF Bay Area and LA. Will have to communicate more with Initech to understand the performance by city so far, as well as scope.

### Power users/ Distribution of Product-Market fit
<img src="https://github.com/tanvidc/Marketplace_startup_eval_VC/blob/master/graphs/distribution.PNG" width="600">
Do few companies make most of the revenue for Initech? According to this cdf, no, and that's usually good! For companies that heavily rely on few big customers (or one, WhatsApp in case of Twilio), losing the client is a high risk. 


### Utilization rate
How well does demand match supply? The only signal from the data we have is perhaps records where an employer or worker exists for a particular month, but has 0 revenue and 0 revenue_minus_direct_costs. Of the ~35K worker records, only ~1K (2.8%) have zero value for both these columns. This under-utilization is a little higher for employers: of the 20.6K records, 2.8K (13%) are zero valued. My guess is that this means that ~13% of postings by employers either didn't find necessary talent, or worker at a rate that was competitive. If the employer was merely present on the platform and hadn't made any service requestes, they are likely considered churn, because otherwise we wouldn't see the large churn and ressurection around holidays. We'd just see lower revenue. I'd clarify all this with Initech. 

## Wrap up thoughts/ Personal Takeaways
I plan to clean up and make this python code portable. There are some SQL resources, and I haven't had a chance to try Mode which might be the best option, but I think there is value in python code that can ingest data for other cases, and generate plots without re-doing plots for each new case study in excel. Although I started this code from scratch in python, in hindsight, I could've considered using SQL code from Jonathan Hsu's GitHub. I haven't analysed rev_minus_direct_costs, and would love to discuss with someone experienced if/how this would be an important metric compared to the things we've already looked at above. Finally, thanks Tribe Capital for this dataset! 
