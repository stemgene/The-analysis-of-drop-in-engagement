# The-analysis-of-drop-in-engagement

## The problem
There is an unexpected downturn in Yammer's user engagement in the month of August, 2014. I have been tasked with identifying the cause of the drop in engagement and must recommend a time-efficient solution.

![user downturn](https://github.com/stemgene/The-analysis-of-drop-in-engagement/blob/main/imgs/user.png)

### How to define engaged user:
Email reaction: 'sent_weekly_digest', 'email_open', 'email_clickthrough','sent_reengagement_email'
Web or APP reaction: 'login', 'home_page', 'view_inbox', 'like_message', 'send_message','search_autocomplete', 'search_run', 'search_click_result'

### Possible reasons:
* Charge fee since August.
* The target users have same groupthink, e.g., holidays. The product faces to companies, maybe lost big companies.
* Portal issue causes some users can't access, e.g., firewall, proxy
* New product from competitor shows up.
* Product issue may cause user leave.
* Fake prosperous before August. It may happen in two situations, short term promotion or fake data.
* Changes of metrics, some traffic from original engagement is split to other channels.

## Hypothesis and Testing Strategies
1. **Technical error**. Was a server or database down? Was there a bad update in the production code? Was there A/B testing in progress that interfered with UX/UI?
  * To test this, I will look for a change in the type of user events with particular interest in homepage landing, email activity, logins, and likes.
  * I will look for different patterns of use between user types (which remain underfined in the instructions)
  * I will look for patterns of use by device type. For example, if there is a bug with a Windows update that prevented Windows users, but not MacOS users from logging in or otherwise engaging with te platform.

2. **Social consequences**. Did the CEO post something inflammatory on Twitter? Was there popular unrest or pandemic? Was it a holiday?
 * I did a Google search for events related to Yammer to see if it was in the news, but found nothing significant.
 * Sept 2, 2014 was the day after labor day in the US but the drop happened prior to the holiday.
 
3. **Business consequences**. Is this a part of a larger business cycle? Was there a corresponding drop in the stock market? Did a competitor increase competition with a new product or feature? Was there a change to user policy?
 * **In July 2014, Yammer made the migration to Sharepoint with Yammer Enterprise as part of the MS Office enterprise suite. A user had to take extra steps to activate their yammer enterprise accounts**
  * "Before you can activate Yammer Enterprise, you need to choose Yammer tool for Sharepoint Online by going to Office365 Admin Center, Sharepoint -> Settings. On the setting page, change the Enterprise Social Collaboration tool to Yammer.com service."
  * There's an additional step and activation hurdle if you already have an office365 personal account.
  * If this is an impactful hurdle for Yammer usage, it will affect Yammer users who have to transition from personal accounts to enterprise accounts due to an activation step. There will be hurdles in the activation process with a large number of pending activations. All devices are likely to be affected proprtionate to their average uses, as are engagement frequency and types.
 * July 24, 2014 a co-founder, David Sacks announced his resignation, but it isn't likely that the typical user would know this or let it impact their Yammer activity.
 * There were no large turns in the stockmarket.
 * I found no significant events in searches related to yammer's competitors having an advantage over yammer.
 * I found no mention of changes to user policy afer Feb 2014, but this would be something to check for internally.
  
## EDA
* Remove duplicates and missing values
* Convert the time to a timestamp column

## Time Series Analysis
### Are accounts that have been made in recent weeks less activethan those activated before July?
If so, I would expect the newer accounts to be less active in August than the older accounts (i.e. the concentration of points in the scatter plot would be thinner in the lower righthand quadrant)
![time of engagement activity](https://github.com/stemgene/The-analysis-of-drop-in-engagement/blob/main/imgs/time%20of%20engagement.png)
I see no thinning in the lower righthand quadrant to support my hypothesis that newly created accounts are less active than long-standing accounts. If anything, they appear to be more active than older accounts across the entire sampling period.

### Dickey-Fuller test to see if the time series is stationary
The ADF statistic is -2.693 and the P-value is 0.075. The data is not so stationary. Then I de-trend the data using the substraction method and substract the baseline from the timeseries. The ADF is -5.944 and the P-value is nearly 0.

### Look for autocorrelation on original data
![autocorrelation](https://github.com/stemgene/The-analysis-of-drop-in-engagement/blob/main/imgs/autocorrelation.png)
![autocorrelation2](https://github.com/stemgene/The-analysis-of-drop-in-engagement/blob/main/imgs/autocorrelation2.png)

In the original data, all but one value is within the 95% confidence interval (blue shading), so there's no autocorrelation (or hidden periodicity), at least for the range of time we are given.
