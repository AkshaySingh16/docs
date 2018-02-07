---
title: Facebook Ads FAQ and Advanced Options
description: An FAQ page of using Branch in your Facebook Ad campaigns.
path: tree/master/src/pages/deep-linked-ads
source: facebook-ads-faq.md
---

# Facebook Ads FAQ and Advanced Options

## FAQ

### What is Facebook MMP?

*"Work with a Facebook Marketing Partner to get deeper insights or measure across several ad networks" ([Facebook - "Measuring for App Ads"](https://developers.facebook.com/docs/app-ads/measuring){:target="\_blank"}).*

The acronym MMP is used to mean either the broad category of Facebook Mobile Marketing Partners, or more narrowly to mean Mobile Measurement Partners. The latter is a special subset of Facebook partners that have access to device-level attribution data. Branch has been vetted by Facebook and joined this group of partners in order to provide both granular analytics and true cross-channel reporting. We help you measure which installs, opens and conversion events should be attributed to Facebook ad campaigns versus other marketing efforts.

### How does Branch attribute events to Facebook ads?

Facebook is a self-attributing network. This means that Facebook claims credit for installs and other events. This differs from some ad networks, which send a stream of impressions and clicks that Branch then matches to events. Branch then compares these claims against other ad networks, as well as traffic coming from email, your website, and other sources, choosing the most recent click to get credit. 

The Branch SDK already helps you track installs and other events. When you enable the Facebook MMP integration, Branch sends events and advertising IDs to Facebook. Facebook then reports whether devices previously viewed or clicked a Facebook ad, including helpful information such as campaign, ad set, and ad. As stated above, Branch then dedupes these claims against other claims for attribution.

### How can I use deep links in Facebook ads?

Creating a deep link is easy! First, make sure you have [set up the integration with Facebook MMP](/pages/deep-linked-ads/facebook-app-install-ads/#enable-facebook-as-an-ad-partner) on the Branch Dashboard. Then navigate to the [Facebook page under Partner Management](https://dashboard.branch.io/ads/partner-management/a_facebook?tab=settings){:target="\_blank"} and click "Create Facebook Link".

Longer instructions can be found in the guides linked to from the [Facebook overview](/pages/deep-linked-ads/facebook-ads-overview/) page. For example, see [this section of the App Installs guide](/pages/deep-linked-ads/facebook-app-install-ads/#create-an-ad-link).

### How can I attribute conversion events to Facebook ads?

First, make sure you have [set up the integration with Facebook MMP](/pages/deep-linked-ads/facebook-app-install-ads/#enable-facebook-as-an-ad-partner) on the Branch Dashboard. Second, [set up tracking for Standard Events](/pages/apps/v2event/#v2-event). It's that simple! We will automatically attribute events to Facebook ads. 

There are advanced options for tracking events, which you can read more about [below](/pages/deep-linked-ads/facebook-ads-faq/#facebook-mmp-event-options).

### What are the permissions you ask for as part of the onboarding process, and why?

| **Permissions (OAuth scopes)** | **Why** |
| - | - |
| ads_read | Pulling marketing insights data (e.g. impressions, clicks) to present on the Branch Dashboard. Also used for pulling creative name and id, etc., to provide richer analytics for installs, opens and other events. |
| business_management | (1) We pull in ad accounts for you to choose from. (2) At the end of the login process, we add our System User to your business and ad account with REPORTS_ONLY permissions. Then we deauthorize the access token that has all 3 of these permissions. In the future, we can easily quarantine/decommission the System User if we detect unusual or unauthorized activity. |

### What is each piece of information needed during the onboarding process, and why?

| **Identifier** | **Why** |
| - | - |
| Ad account | Pulling marketing insights data (e.g. impressions, clicks) to present on the Branch Dashboard. |
| Facebook App ID | Sending installs, opens and other events to Facebook in order to see whether they were driven by a Facebook ad campaign. |

### I'm having problems finding or choosing the correct ad account(s)

#### The ad account I want to select is greyed out

![Not admin](/img/pages/deep-linked-ads/facebook-ads-faq/not-business-admin.png)

If you are not an admin of the *business* linked to an ad account, you will not be able to add it. This is because we will not be able to add our System User for attribution and analytics purposes. To check whether you are a business admin, please visit the [business's settings page](https://business.facebook.com/settings/people){:target="_blank"}. If you can see yourself listed, and you can see that your role is shown as admin (see image below), you should be able to complete setup. Otherwise, please request that an admin at your business complete the setup on the Branch Dashboard.

![admin](/img/pages/deep-linked-ads/facebook-ads-faq/business-admin.png)

If you still have questions, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Business Admin" in the subject.

#### I see a warning underneath my ad account saying that I need to be an admin

![warning about admin](/img/pages/deep-linked-ads/facebook-ads-faq/standalone-ad-account.png)

If an ad account is not linked to a business, then we cannot guarantee that this account setup will succeed. Please visit [the ad account settings page](https://www.facebook.com/ads/manager/account_settings/information/), navigate to the appropriate ad account, and ensure you are an admin (see image below). 

![Ensure admin](/img/pages/deep-linked-ads/facebook-ads-faq/adaccount-settings.png)

If you still have questions, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Standalone Ad Account(s)" in the subject.

#### I can't see the ad account I want to use at all

Please try logging out and logging back in on Facebook. Note the email address that you use. If you still do not see ad accounts, please visit [business.facebook.com](https://business.facebook.com) and ensure that you use the same email address / Facebook account. If you still cannot figure this out, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Missing Ad Account(s)" in the subject.

### What is the difference between your previous Facebook Ads product, and the new Facebook Ads product?

Branch is now a Facebook Mobile Measurement Partner (MMP). This means we are partnering with Facebook to more accurately attribute your installs, opens and custom events back to Facebook ad campaigns! 

The major differences: we can use this product with a Branch deep link. No need to manually create Branch links and add them to Facebook ads! 

If you use a Branch deep link, we will still return the Branch deep link information in app so that you can deep link your users to content. Attributed events will *not* have the Branch deep link information, but rather the Facebook ad campaign information. This info cannot be passed along to third parties via our Data Integrations.

### Can I get the data out?

!!! Warning
	Data Integrations will never include events attributed to Facebook. This is because we cannot share device-level Facebook attribution data with third parties.

There are many ways to access data pertaining to Facebook. 

You can see analytics on impressions, clicks, installs, opens and conversion events on various pages of the [Branch Dashboard](https://dashboard.branch.io){:target="\_blank"}, as well as the [Query API](pages/exports/query-api).

If you have signed Facebook's ["Advanced Mobile Measurement" agreement ("Data Use Terms for Advanced Mobile App Measurement")](https://www.facebook.com/ads/manage/advanced_mobile_measurement/tos){:target="\_blank"}, then you can get device level data out via [Webhooks](pages/exports/ua-webhooks/), the [Data Export API](pages/exports/api-v3/), and [CSV Exports](https://dashboard.branch.io/data-import-export/csv-exports){:target="\_blank"}. If you have not signed this agreement, any event attributed to a Facebook ad will look like an organic event when accessed via Webhooks, the Data Export API, and CSV Exports.

We cannot send device-level Facebook attribution data to third parties. Thus we cannot send events attributed to Facebook via Data Integrations. Please instead consider analyzing this data in-house (using Webhooks, the Data Export API, or CSV Exports), or using the Branch Dashboard for all of your analytics and attribution needs. If you have analytics needs that are not met by the Branch Dashboard, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Feature Request" in the subject.

| **Branch feature** | **Facebook data included** |
| - | - |
| [Dashboard visualizations](https://dashboard.branch.io/){:target="\_blank"} | Pre-aggregated analytics |
| [Query API](pages/exports/query-api/) | Pre-aggregated analytics |
| [Liveview](https://dashboard.branch.io/liveview){:target="\_blank"} | Device-level analytics * |
| [Data Export API](pages/exports/api-v3/) | Device-level analytics * |
| [CSV Exports](https://branch.dashboard.branch.io/data-import-export/csv-exports){:target="\_blank"} | Device-level analytics * |
| [Webhooks](pages/exports/ua-webhooks/) | Device-level analytics * |
| [Data Integrations](pages/integrations/data-integrations/) | Not supported |

(*) You must have signed you have signed Facebook's ["Advanced Mobile Measurement" agreement ("Data Use Terms for Advanced Mobile App Measurement")](https://www.facebook.com/ads/manage/advanced_mobile_measurement/tos){:target="\_blank"} to view this data

### The data on Facebook and the data on Branch does not line up!

Please see the section below, [Sources of Discrepancies between Facebook and Branch](pages/deep-linked-ads/facebook-ads-faq/#sources-of-discrepancies-between-facebook-and-branch).

## Facebook Ads Advanced Options

### Facebook MMP event options

!!! Note
	To see the options below on the Branch Dashboard, [click here](https://dashboard.branch.io/ads/partner-management/a_facebook?tab=events){:target="\_blank"}.

Branch + Facebook MMP allows you to attribute events back to your Facebook ad campaigns. Branch sends events to Facebook, along with metadata including advertising ID. Facebook then returns info on the ad that the user last viewed or clicked, if any. Branch then surfaces this on our Dashboard, and conditionally* makes this data available in our [Data Feeds](/pages/exports/data-feeds/) product.

Partners have several options when it comes to sending events to Facebook. These are discussed below.

 (*) You must have signed the [Data Use Terms for Advanced Mobile App Measurement](https://www.facebook.com/ads/manage/advanced_mobile_measurement/tos){:target="\_blank"}

#### Tracking installs

Branch sends all installs to Facebook. Facebook de-duplicates installs on their end. If you have the Facebook SDK and/or another MMP, these also send installs to Facebook's backend. This will not result in duplicate installs, since Facebook de-dupes them.

#### Tracking reinstalls and opens

!!! Warning
	Facebook does not de-duplicate custom app events on their backend. So if you have the Facebook SDK integrated or another MMP tracking app opens, choose option 1 below.

When tracking reinstalls and opens, you have 3 options:

1. *use Branch name (branch_open)*: This allows us to get attribution data from Facebook, but without it counting as an app open. Use this option if you have the Facebook SDK integrated or are testing with another MMP. Since the Facebook SDK or other MMP is already sending fb_mobile_activate_app, you do not want Branch to send this a second time. (Default)
2. *use Facebook name (fb_mobile_activate_app)*: Branch will send the exact event used by Facebook for tracking app opens. Use this option if you do not have the Facebook SDK and you are not tracking opens with another MMP, and you would like Branch to help Facebook record opens.
3. *disable*: Use this option if you do not want Branch attributing opens at all. In some cases, we may still be able to attribute opens based on previously retrieved attribution data from Facebook. But we will not send any opens to Facebook in order to get attribution data back.

#### Tracking other conversion events

!!! Warning
	Facebook does not de-duplicate custom app events on their backend. If you are tracking conversion events with the Facebook SDK or another MMP, choose option 1 below.

It's possible to track app events using only Branch! You can [track the events](/pages/apps/v2event/#v2-event) with Branch once, and then we send them to Facebook as well as other analytics systems. Use the [v2/event logging methods](/pages/apps/v2event/#v2-event) outlined here.

When tracking add to cart, purchase, and other Facebook app events, you have 3 options:

1. *use Branch name*: This allows us to get attribution data from Facebook, but without it counting as a purchase, add to cart, etc. Use this option if you have the Facebook SDK integrated or are testing with another MMP, and you already track app events via one of those two methods. Since the Facebook SDK or other MMP is already sending events to Facebook, you do not want Branch to send these a second time. (Default)
2. *use Facebook name*: Branch will send the exact event used by Facebook for tracking app events. Use this option if you are not already tracking app events with the Facebook SDK or another MMP, and you would like Branch to help Facebook record these events.
3. *disable*: Use this option if you do not want Branch attributing these conversion events. In some cases, we may still be able to attribute these conversion events based on previously retrieved attribution data from Facebook. But we will not send any conversion events to Facebook in order to get attribution data back.

#### Mapping of Branch event names to Facebook events

| Branch event name | Facebook MMP _eventName
| --- | ---
| ACHIEVE_LEVEL | fb_mobile_level_achieved
| ADD_PAYMENT_INFO | fb_mobile_add_payment_info
| ADD_TO_CART | fb_mobile_add_to_cart
| ADD_TO_WISHLIST | fb_mobile_add_to_wishlist
| COMPLETE_REGISTRATION | fb_mobile_complete_registration
| COMPLETE_TUTORIAL | fb_mobile_tutorial_completion
| INITIATE_PURCHASE | fb_mobile_initiated_checkout
| PURCHASE | fb_mobile_purchase
| RATE | fb_mobile_rate
| SEARCH | fb_mobile_search
| SPEND_CREDITS | fb_mobile_spent_credits
| UNLOCK_ACHIEVEMENT | fb_mobile_achievement_unlocked
| VIEW_ITEM | fb_mobile_content_view

#### Mapping of Branch metadata to Facebook metadata

|Branch Key-Value Pair | Facebook MMP Key-Value Pair | Facebook event(s) supported
| --- | --- | ---
|commerce_data.revenue | _valueToSum | fb_mobile_add_to_cart, fb_mobile_add_to_wishlist, fb_mobile_initiated_checkout, fb_mobile_purchase, fb_mobile_spent_credits, fb_mobile_content_view
|commerce_data.currency | fb_currency | fb_mobile_add_to_cart, fb_mobile_add_to_wishlist, fb_mobile_initiated_checkout, fb_mobile_purchase, fb_mobile_content_view
|content_items[0].$sku | fb_content_id | fb_mobile_add_to_cart, fb_mobile_add_to_wishlist, fb_mobile_tutorial_completion, fb_mobile_initiated_checkout, fb_mobile_purchase, fb_mobile_rate, fb_mobile_spent_credits, fb_mobile_content_view
|content_items[0].$product_category | fb_content_type | fb_mobile_add_to_cart, fb_mobile_add_to_wishlist, fb_mobile_initiated_checkout, fb_mobile_purchase, fb_mobile_rate, fb_mobile_search, fb_mobile_spent_credits, fb_mobile_content_view
|content_items[0].$quantity | fb_num_items | fb_mobile_initiated_checkout, fb_mobile_purchase
|content_items[0].$rating | _valueToSum | fb_mobile_rate
|content_items[0].$rating_max | fb_max_rating_value | fb_mobile_rate
|event_data.search_query | fb_search_string | fb_mobile_search
|content_items[0].$og_description | fb_description | fb_mobile_achievement_unlocked
|custom_data.fb_payment_info_available | fb_payment_info_available | fb_mobile_initiated_checkout
|custom_data.level | fb_level | fb_mobile_level_achieved
|custom_data.fb_success | fb_success | fb_mobile_add_payment_info, fb_mobile_tutorial_completion, fb_mobile_search
|custom_data.fb_registration_method | fb_registration_method | fb_mobile_complete_registration

Currently Facebook appears to only support sending one fb_content_id (etc) per event, whereas Branch allows you to send many. To provide as much functionality as possible, we choose the first content_item and search it for key-value pairs that can be sent to Facebook.

#### Tracking custom events

In addition to tracking installs and Facebook app events (see [Tracking other conversion events](#tracking-other-conversion-events) above), you can also have Branch attribute custom events. To do so, we must send those events to Facebook.

When tracking custom events that have no equivalent [Facebook App Event](https://developers.facebook.com/docs/marketing-api/app-event-api){:target="\_blank"}, you have 2 options:

1. *enable*: Branch will send custom events to Facebook. this allows us to get attribution data from Facebook. (default)
2. *disable*: Use this option if you do not want Branch attributing custom events. In some cases, we may still be able to attribute these custom events based on previously retrieved attribution data from Facebook. But we will not send any custom events to Facebook in order to get attribution data back. 

### Migrating from the existing Facebook integration to MMP

!!! Note
	You can no longer see the previous Facebook onboarding flow that required you to copy-paste your Facebook app secret. Please use the "Authenticate with Facebook" option instead.

If you have been using our integration with Facebook prior to February 14, 2018, then we highly recommend that you upgrade to our new integration that includes MMP. 

We are now certified by Facebook as a Mobile Measurement Partner! Branch can now help you attribute installs, opens, and conversion events to Facebook like never before.

This integration includes full support for Facebook, Instagram, and the Audience Network. We also automatically pull in impressions and clicks from Facebook and surface those alongside your clicks on Branch links. The deep linking experience your users love is still supported. 

Instructions on how to get set up with Facebook MMP are [here](/pages/deep-linked-ads/facebook-app-install-ads/#enable-facebook-as-an-ad-partner). Note that this will replace your existing credentials on our backend. Instead of copy-pasting your Facebook app secret into the Branch Dashboard, you can now simply click through the normal Facebook login flow.

Branch will now automatically surface Facebook campaign, ad set, and ad information on the Branch Dashboard's visualizations! This isn't limited to [Ads Analytics](https://dashboard.branch.io/ads/analytics){:target="\_blank"} -- it also includes cross-channel analytics such as [Source Analytics](https://dashboard.branch.io/sources){:target="\_blank"}.

### Sources of Discrepancies between Facebook and Branch

When using Branch as your Facebook MMP, you may notice some data discrepancies between the Branch dashboard and the Facebook dashboard if not configured correctly. We have highlighted several sources of discrepancies if they are present after you have onboarded with Facebook on the Branch dashboard. 

There are many reasons why you may see different numbers on Facebook and Branch. Please note that we have one system for tracking impressions and clicks (via the Facebook Insights API) and a different system for tracking installs, reinstalls, opens and conversion events (via a private Facebook API). When trying to figure out differences, it's best to pick one event at a time (e.g. clicks or installs) and focus on causes of discrepancies there.

The first two sections below covers common causes of discrepancies: attribution windows and timezones. The following sections then provide more steps on diagnosing and troubleshooting specific problems.

#### Attribution Windows

An attribution window is the maxiumum amount of time between an initial action (click or impression) and a conversion event (install or open) for which you attribute that conversion event as occuring _because of_ that initial action.

Example with 3 day view attribution window: If a user views your ad and 2 days later installs your app, that install would be attributed to that ad view. However if the user views your ad and 4 days later installs the app, that install would be considered an organic install and would NOT be attributed to that ad view.  You can read more in our documentation here: https://docs.branch.io/pages/dashboard/unified-analytics/#attribution-windows

If one of your attribution windows on the Branch dashboard is different than the corresponding window on the Facebook dashboard, the data between the two will not align. You can mitigate this by changing one of more of your attribution windows on the Branch dashboard, or changing your Facebook dashboard for the given ad account.

There are four Branch attribution windows, and two Facebook attribution windows. This chart shows which Facebook window name each Branch window name corresponds to:

| Branch window name  |  Facebook window name |
|---|---|
| Click to install | Click Window|
| Click to session start |  Click Window |
| Click to conversion event | Click Window |
| Impression to install | View Window |
| Impression to session start | View Window |
| Impression to conversion event | View Window |

*Change your Facebook attribution windows*
In order to update your Facebook Attribution window for a particular ad account, you can go to https://business.facebook.com/ads/manager/account_settings/information. Choose the account in the dropdown in the upper-left corner. As long as you're an admin on that account, you should see a section 'Attribution' at the top-right, and an ability to edit the Click or View window or both.

*Change your Branch attribution windows*
Alternatively or in addition, you could update any of your four Branch attribution windows. To do so go to the [Link Settings](https://dashboard.branch.io/link-settings) section of the Branch dashboard, and scroll down to the 'Attribution Windows' section and expand it. Alter any of the four windows listed in the chart above to match the corresponding Facebook window, and then save at the bottom of the page.

*Reporting based on time of impression or time of conversion*

Facebook and Branch may report the same install as occurring on different days, if the impression is on one day but the install is on another day.

Background:

Facebook by defaults reports installs based on the day that the impression occurred. They also allow you to see reports based on the day that the install occurred.

Branch always reports installs based on the date of install, never the date of impression.

Let's illustrate this with a scenario:

User views an ad on Apil 1, clicks it, then installs the app on April 2.

By default, Facebook reports the install as occurring on April 1. However, when pulling data from the insights API, you can specify option action_report_time=conversion. This causes Facebook to report that the install occurred on April 2.

Branch will always report the install as having occurred on April 2.

#### Timezones

Please make sure the timezone is the same for your Facebook ad account and your Branch account. 

You can see the timezone used by your Branch account [here](https://dashboard.branch.io/account-settings/app){:target="\_blank"}.

You can see the timezone used by your Facebook ad account [here](https://www.facebook.com/ads/manager/account_settings/information/){:target="\_blank"}. If you are using multiple ad accounts with Branch, be sure to align the timezones of each of them.

If you are unable to align all timezones, you may notice some data on the Branch Dashboard does not line up exactly with data on the Facebook Dashboard. However, data will not be lost, but merely shifted between days. Summing figures over longer periods of time should greatly diminish the effect of having inconsistent time zones.

#### Discrepancies with Impressions and Clicks

##### 1. I don't see any clicks or installs on the Branch Dashboard

First, be sure you've set up the Facebook integration! Work through [these steps](pages/deep-linked-ads/facebook-app-install-ads/#enable-facebook-as-an-ad-partner) and ensure you reach the bottom. You should have at least one ad account enabled, and a Facebook app id listed.

Second, make sure you're running ads that are resulting in installs, reinstalls, or opens. Once you see installs, you should shortly start seeing clicks. For more, see the next FAQ item.

If you're unable to see installs, reinstalls, or opens on the Branch Dashboard, skip down to the section below: [I don't see any installs, reinstalls or opens on the Branch Dashboard](pages/deep-linked-ads/facebook-ads-faq/#1-i-dont-see-any-installs-reinstalls-or-opens-on-the-branch-dashboard).

##### 2. I see installs on the Facebook Dashboard, but no clicks

!!! Note
	Branch will only show impressions and clicks for campaigns that have installs, reinstalls, or opens. If you have campaigns that have not resulted in these app-based outcomes, we will hide them. This is to prevent massively inflating analytics on the Branch Dashboard with data that is not relevant. If you have feedback on this, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + clicks" in the subject.

If you turned on the integration within the last hour, then you may need to refresh the Branch Dashboard to see clicks. We automatically start a background job to pull in impressions and clicks from Facebook the first time you visit the [Ads Analytics](https://dashboard.branch.io/ads/analytics){:target="\_blank"} page after enabling Facebook.

If it has been longer than an hour since you (1) enabled the MMP integration then (2) visited the Ads Analytics page then (3) pressed refresh and (4) see installs but still no clicks, then please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and put "Facebook MMP + 0 clicks" in the subject. Please include: 

* Branch app id
* Facebook ad account id
* One Facebook campaign name for which you have clicks and installs
* Date range
* For every day in date range, the number of clicks Facebook is reporting for this campaign - include both a table and a screenshot
* For every day in date range, the number of installs Facebook is reporting for this campaign - include both a table and a screenshot


##### 3. I see clicks on the Branch Dashboard, but the numbers look different from what I see on the Facebook Dashboard.

*If you are looking at impressions/clicks for the current day:*

If the numbers line up pretty closely between Branch and Facebook, then it's possible the Facebook numbers are slightly more recent. The Facebook Insights API refreshes every 15 minutes. Branch tries to pull updated numbers as often as possible.

If the numbers do not line up closely, but you recently started a new campaign, it may be that Branch has not yet pulled in data for that campaign. The numbers should line up much more closely within an hour. If they do not, then please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and put "Facebook MMP + Click Dicrepancies" in the subject. Please include: 

* Branch app id
* Facebook ad account id
* One Facebook campaign name for which you have clicks and installs
* Date range
* For every day in date range, the number of clicks Facebook is reporting for this campaign - include both a table and a screenshot
* For every day in date range, the number of installs Facebook is reporting for this campaign - include both a table and a screenshot 

*If you are looking at impressions/clicks for a past day:*

When you initially enable the Facebook integration, then visit the [Ads Analytics](https://dashboard.branch.io/ads/analytics){:target="\_blank"} page, Branch will start fetching impressions and clicks for the most recent several days. If you go back beyond 7 days, we may not have impressions and click data. If you need this data, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Loading Old Clicks" in the subject. Please include:

* Branch app id
* Facebook ad account id
* One Facebook campaign name for which you have clicks and installs
* Date range

#### Discrepancies with Installs, Opens and Conversion Events

##### 1. I don't see any installs, reinstalls or opens on the Branch Dashboard

First, be sure you've set up the Facebook integration! Work through [these steps](pages/deep-linked-ads/facebook-app-install-ads/#enable-facebook-as-an-ad-partner) and ensure you reach the bottom. You should have at least one ad account enabled, and a Facebook app id listed.

Second, make sure you're running ads that are resulting in installs, reinstalls, or opens.

Third, on the Facebook Dashboard, locate a campaign with installs, reinstalls, or opens. Determine the ad account id for which you are running an app campaign. Then navigate to the [Facebook page under Partner Management](https://dashboard.branch.io/ads/partner-management/a_facebook?tab=settings){:target="\_blank"} and make sure that ad account id is listed as part of the completed signup process. It should appear here (two ad accounts are shown as enabled in the screenshot, though the ad account ids are blurred out):

![complete](/img/ingredients/deep-linked-ads/enable-facebook-ad-partner/9-complete.png)

Fourth, make sure you have installs, reinstalls, or opens that have occurred after you enabled the Branch + Facebook integration. We cannot pull historical device-level data, as that's not how the Facebook APIs are architected. You should enable Branch + Facebook, wait for new installs to occur, then check the [Ads Analytics](https://dashboard.branch.io/ads/analytics){:target="\_blank"} page.

If after all this you're still not seeing installs, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + 0 installs" in the subject. Please include:

* Branch app id
* Facebook ad account id
* One Facebook campaign name for which you have installs
* Date range
* For every day in date range, the number of installs Facebook is reporting - include both a table and a screenshot

##### 2. I see installs, reinstalls or opens on the Branch Dashboard, but the numbers look different from what I see on the Facebook Dashboard

If you've made it this far, the integration between Branch + Facebook is at least somewhat functional! Time to identify why numbers are not lining up.

Try comparing (1) just installs, and (2) just for one campaign. On the Branch [Ads Analytics](https://dashboard.branch.io/ads/analytics){:target="\_blank"} page, you can view data for just one campaign by choosing "Add Filter", selecting "campaign" from the first dropdown, and the individual campaign name from the second dropdown. Again, try to get numbers to line up between Facebook and Branch just for installs on one campaign.

First, make sure the attribution windows line up between Facebook and Branch. You can read more on this [above](pages/deep-linked-ads/facebook-ads-faq/#attribution-windows).

Second, make sure the timezones line up between Facebook and Branch. You can read more on this [above](pages/deep-linked-ads/facebook-ads-faq/#timezones).

Note that attribution windows are not applied to events that occurred in the past. So if you have a 30-day attribution window for click-to-install on Branch, and a 7-day window for clicks on Facebook, once you change the Branch click-to-install attribution window to 7 days, it will not automatically update historical numbers. Instead, you'll need to wait for new installs to occur under the stricter 7-day Branch click-to-install attribution window. The next day you should be able to come back and look at just the current day's install numbers, and they should line up more closely.

If after all this you're still seeing discrepancies, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Install Discrepancies" in the subject. Please include:

* Branch app id
* Facebook ad account id
* One Facebook campaign name for which you have clicks and installs
* Date range
* Your Facebook attribution window - include both a table and a screenshot
* For every day in date range, the number of installs Facebook is reporting - include both a table and a screenshot
* For every day in date range, the number of installs Branch is reporting - include both a table and a screenshot

!!! Note
	In some rare cases, we've seen partners running multiple Facebook campaigns with the same name. In this case, the Branch Dashboard will combine stats for all of these campaigns under the same name. We still retain this data separately on our backend, as there are different Facebook campaign ids. While we do not expose this on the Branch Dashboard, you can pull statistics by campaign id via the [Query API](pages/exports/query-api).

##### 3. I don't see any conversion events on the Branch Dashboard

Be sure you are tracking v2/events - [learn more from our v2/event docs](pages/apps/v2event/#v2-event).

Be sure you are opting to send conversion events to Facebook - learn more from the section [Facebook MMP event options](pages/deep-linked-ads/facebook-ads-faq/#facebook-mmp-event-options) above.

Be reasonably confident that users coming from Facebook ads are completing conversion events. If you have, for example, only a small percentage of users completing purchases, and only a small percentage of users downloading your app from Facebook, it's possible that there is no overlap between users making purchases and users coming from Facebook.

If after all this you're still seeing discrepancies, please [contact us](https://support.branch.io/support/tickets/new){:target="\_blank"} and include "Facebook MMP + Install Discrepancies" in the subject. Please include:

* Branch app id
* Facebook ad account id
* One Facebook campaign name for which you have clicks and installs
* Date range
* Your Facebook attribution window - include both a table and a screenshot
* For every day in date range, the number of installs Facebook is reporting - include both a table and a screenshot
* For every day in date range, the number of installs Branch is reporting - include both a table and a screenshot
* For every day in date range, the number of conversion events Facebook is reporting - include both a table and a screenshot
* For every day in date range, the number of conversion events Branch is reporting - include both a table and a screenshot

##### 4. I see conversion events on the Branch Dashboard, but the numbers look different from what I see on the Facebook Dashboard

We have not encountered any issues here so far. Please see [I see installs, reinstalls or opens on the Branch Dashboard, but the numbers look different from what I see on the Facebook Dashboard](pages/deep-linked-ads/facebook-ads-faq/#1-i-dont-see-any-installs-reinstalls-or-opens-on-the-branch-dashboard) for steps to follow, and for information to send to us if we need to debug together.
