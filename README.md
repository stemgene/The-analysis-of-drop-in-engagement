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
