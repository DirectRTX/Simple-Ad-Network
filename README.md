# Simple Ad Network
Simple Ad Network is a free, open source PHP script to start your own ad network.  This script was developed by the team at <b><a target="_blank" href="https://directrtx.com">DirectRTX</a></b> to allow anyone to start their own popunder network or media buying system.

Our #1 goal when developing this script was to allow anyone to start their own network for less than $10/month and make sure they never have to spend more than that until they're earning at least $5,000/day.  Seriously, you should be making at least $5000/day before you have to invest more than $10/month for hosting.

Please read the full documentation before setting up your own network.  If you've ever installed a script like WordPress - this will be just as easy.  But there's a lot of moving parts to make sure that your network can easily handle hundreds of millions of hits per day.  Below we'll walk you through every step of getting setup and explain how everything works.

This documentation is pretty long.  But - you can actually get your entire network fully setup and running in less than 60 minutes by following these instructions.  Don't believe us?  Time it.  Seriously, it'll be done within 60 minutes.

By the way, this is one badass system.  It can handle unlimited traffic, has a built-in affiliate program, and provides publishers with multiple ways (popunders, direct links, etc) to send traffic.  There's nothing else like it.  And it's free.

## How You'll Make Money
We know that's what you're here for, so let's get right to it.

Your ad network will be able to handle an unlimited amount of publishers.  All of the traffic is going to be routed using CloudFlare, so the traffic itself never even hits your server.  Managing multiple clusters of servers handling hundreds of millions of hits per day can be a huge task - we've handled that for you.

First the traffic will be sent to DirectRTX.  The automatic postback system at DirectRTX will automatically ping your system whenever traffic is purchased and your system will automatically credit it to the correct publisher's account.  So, you'll make money by paying a percent of that money to publishers and keeping a percent for yourself.

Additionally, you'll have options to monetize the traffic that DirectRTX doesn't purchase - which is where you can make a ton of money.  If a publisher doesn't set a fallback URL (around half of them tend not to), you'll be able to set a default URL where all that unsold traffic gets sent to.  Any money you earn from these networks will be 100% profit for you - most networks don't have features like DirectRTX, so there's no way to credit that money to publishers.

Before you start assuming this is shady - remember, this tends to be standard practice in the popunder world - espcially when publishers are given the chance to set their own fallback URL.  If a network doesn't have direct advertisers for traffic, they just sell it off to other networks and keep the profit.  Don't worry, this is all about making money :)

Oh, and at the end of this, we're even going to teach you how to promote the network.

## What You Need to Get Started
Please make sure you have the following things before you get started:

1.  A domain name.  We recommend using <a target="_blank" href="https://www.namesilo.com">NameSilo</a>.
2.  A web hosting account.  We recommend <a target="_blank" href="https://www.namecheap.com/hosting/shared/">NameCheap</a>.
3.  An account at <a target="_blank" href="https://directrtx.com">DirectRTX</a>.  Instantly approved.
4.  A free account at <a target="_blank" href="https://www.cloudflare.com">CloudFlare</a>.  No upgrades needed.
5.  A <a target="_blank" href="https://www.paypal.com/">PayPal</a> account.  Used for payments from DirectRTX.

You can use any web hosting company you want, but make sure this script is the only thing installed in the account.  It was developed using NameCheap so we know it works perfectly there.  Just make sure that whatever hosting company you use has PHP and MySQL (or MariaDB) available - also, it needs to run on Apache if possible.

So, let's get started setting up everything below.  We'll use our suggestions as examples, but feel free to use whatever domain registrar and hosting company that you want.

### Register Your Domain Name

Your domain name is your brand, but we shouldn't have to teach you that.  Look at some of the names of other popunder networks and come up with something unique.  Once you've found a good domain name, register it at NameSilo.

Please don't email asking for suggestions, we don't care what you name your network.

### Create A Web Hosting Account

Go to NameCheap and signup for the cheapest plan.  After creating your account, they will provide you with your nameservers.  Nameservers are used to point a domain name to the server it's hosted.  So, go back to the company you registered your domain name with and change the nameservers for your domain to the ones provided by NameCheap.

### Signup at DirectRTX.com

Go to DirectRTX.com and create an account.  It's simple and doesn't even require email verification.

Once you've created your account, you'll need to login and do 2 things.  Make sure you pay attention here:

1.  Go to the "My Links" section and you'll see your unique link.  In that link is a 6 digit number - write it down.
2.  Go to https://directrtx.com/postback-settings.php and enter the following URL:

```http://example.com/postback.php?subid=[subid]&revenue=[revenue]&secretkey=XXXXXXXXXX```

Replace `example.com` with your domain name (without www).  Replace with `XXXXXXXXXX` with a unique 15-digit code.  You can use <a target="_blank" href="https://passwordsgenerator.net/">PasswordGenerator.net</a> to generate this code - just make sure it's only letters and numbers, no special characters.  The unique code is to make sure nobody can send fake postbacks to credit their account.  Don't share it with anyone.

### Getting Setup At CloudFlare

This is the most complicate step you'll perform during the setup process - that should tell you this who process is going to be pretty damn easy.  Remember, CloudFlare and DirectRTX are the reason you'll be able to handle hundreds of millions of hits on a daily basis, so it has to be setup correctly.  So, let's get started:

1.  Go to CloudFlare.com and register an account.

2.  During the registration process, you'll need to add your domain.

3.  For your domain to be activated, you'll need to change the nameservers at your domain registrar (again) to point to the ones CloudFlare provides you with.  We first pointed them to your hosting company so CloudFlare can grab the correct DNS records and automatically point to your domain to your hosting company as well.

Once you've completed the 3 steps above, your account and domain are setup at CloudFlare.  But it doesn't end there.  To make the magic happen, we'll need to do 2 more things:  create a CNAME record and setup Page Rules.

<b>How to Create CNAME Records</b>

Select your domain and go to the "DNS" tab in CloudFlare's dashboard.

When adding a record, you have the option to select or enter 4 fields.  Add this record:

`CNAME` `go` `whitelabel.directrtx.com` `Automatic TTL`

After it is added, make sure there's an orange cloud next to it.

You're done setting up the required DNS record.  It really wasn't that difficult was it?

<b>How to Create Page Rules</b>

Go to the Page Rules tab in CloudFlare's dashboard.

You're going to create 3 pages - all of them are going to use the `Forwarding URL` setting.  Also, they will all use the `Status Code` 301. Now that you know those 2 settings are used by all 3 page rules, create these:

<b>URL Match Line #1:</b> `*go.example.com/*/?fb=*`  
<b>Destination URL #1:</b>  `http://directadserver.com/[DIRECTRTX-ID]/?subid=$2&fb=$3`

<b>URL Match Line #2:</b> `*go.example.com/*/*`  
<b>Destination URL #2:</b>  `http://directadserver.com/[DIRECTRTX-ID]/?subid=$2&fb=[FALLBACK-URL]`

<b>URL Match Line #3:</b> `*go.example.com/*`  
<b>Destination URL #3:</b>  `http://directadserver.com/[DIRECTRTX-ID]/?subid=$2&fb=[FALLBACK-URL]`

Here's a description of what each Page Rule is doing:

<b>Page Rule #1 -</b> Passes along your publisher's Fallback URL whenever they've entered one.  
<b>Page Rule #2 -</b> Automatically enters your Fallback URL whenever a publisher doesn't set their own.  
<b>Page Rule #3 -</b> Catches all traffic that doesn't include a publisher's ID number and redirects it.

You will need to replace these three things in each of the rules above (while you're adding them):

`example.com` - Replace this with your own domain name.  Do not remove the `go.` subdomain.  
`[DIRECTRTX-ID]` - Replace this with your 6-digit ID number that you got earlier from DirectRTX's dashboard.  
`[FALLBACK-URL]` - Replace this with YOUR fallback URL - where you want unsold traffic to go to.

It is VERY important that the Page Rules are listed in CloudFlare's dashboard in the same order we have them listed above.  If they aren't your system will NOT work properly.  You can rearrange them by dragging the page rules in their dashboard.

We're going to talk more about the Fallback URL in the next section.  Please read it carefully.

But you're done setting up CloudFlare at this point!  Woohoo!

<b>Using A Default Fallback URL</b>

First and foremost, your Fallback URL should be URL Encoded.  So, after you choose what you want your Fallback URL to be, go to <a target="_blank" href="https://www.urlencoder.org/">URL Encoder</a> and encode it.  The encoded version is what needs to be used in your Page Rules.

For your Fallback URL, you have 4 options to choose from (from simplest to most complicate):

1.  <b>Set it as your ad network's homepage.</b>  Any unsold traffic will be sent there and advertise your network.  You won't earn money directly from this traffic, but some people may signup and earn money for you.

2.  <b>Send the traffic to a single network.</b>  There are plenty of networks like PopCash, Propeller Ads, and ZeroPark that will provide you with a direct link that you can send the unsold traffic to and make money.

3.  <b>Send the traffic to <a target="_blank" href="https://www.adspyglass.com/">AdSpyGlass</a>.</b>  This is an ad mediation network that will automatically forward your traffic to the network its algorithm detects will pay the most for that specific visitor.  It will also send unsold traffic from one network to the next using a waterfall system (described below).

4.  <b>Setup your own waterfall system.</b>  You can signup for multiple networks that provide both direct links and fallback URLs.  For example, you can set Network #1's fallback URL as the direct link from Network #2 and set the fallback URL for Network #2 as the fallback URL from Network #3 and so on.  But in our opinion, it's easier to just use AdSpyGlass to handle all of that for you - they are free and take 10% of your traffic for using their service.

In our experience, AdSpyGlass has pretty shitty support - if you get a response at all.  So while the idea behind the service is good, we make no guarantees that you'll receive any sort of assistance from them.

How you choose to handle unsold traffic is completely up to you.  You may be able to find more unique ways to monetize it and that's totally your decision.  These are just the most popular methods people use.

## Let's Take A Break For A Minute

Wow!  If you've reached this point, you're actually almost done!  And you haven't had to do any complicated coding.  You've just had to make a few decisions and change some settings in various control panels.

At this point in time, you should take a moment to review everything you've done above.  If it's done correctly, the system will work perfectly and be able to handle hundreds of millions of hits per day.  But even the smallest error can cause the entire system to break.  So, please take a moment to review everything above.  We know it's a lot, but please do it.

## Setting Up Your Database

We're going to assume that you're using a web hosting company that uses cPanel.  But even if you're not, these instructions should still work for most hosting companies.

You'll need to login to your control panel and go to MySQL Databases.  Create a database AND add a user to the database.  Adding a user is very important.  If you don't add one, you won't be able to connect to the database.

Now, go to phpMyAdmin (in cPanel) and select the database you just created.  Once your database has been selected, click on "Import" in the top navigation.  Upload the `database.sql` file that's downloadable from above.

Congrats!  Your database has been setup and you'll never have to mess with it again.

## Uploading Your Website's Files

Now it's time to get your website's files upload.  You can download this Github repository by <a target="_blank" href="https://github.com/DirectRTX/Simple-Ad-Network/archive/master.zip">clicking here</a>.

This will download the entire repository, but you just need to upload all of the files from the `UPLOAD` directory to your `public_html` folder.  Please note, you don't need to upload the `UPLOAD` directory itself, just upload all of the files that are inside of it.  I suggest using FileZilla to upload the files quickly.

## Changing Configuration Settings

You are going to need to edit each line of your `config.php` file.  Here's an explanation of each variable:

These are your MySQL settings and are used on every page to connect to your database.

- <b>$hostname =</b> The name hostname for connecting to MySQL.  Normally this is "localhost". 
- <b>$username =</b> The user you created and added to your MySQL database. 
- <b>$password =</b> The password for the above MySQL user.  Not your cPanel password. 
- <b>$database =</b> The name of your MySQL database.  Case sensitive. 

These are the keys you've generated.  We suggest that you make them 15 characters each.  Do not use special characters.  These fields are case sensitive.  You should make each key different.

- <b>$admin_key =</b> This is the secret key you'll use to access the admin area.
- <b>$postback_key =</b> This is the secret key we use for sending you postback information.
- <b>$cronjob_key =</b> This is the secret key that's used to run your cron jobs.

These are the settings used on your website, such as the company name and homepage text.

- <b>$directrtx_id =</b> This is your 6-digit ID number from DirectRTX's dashboard.
- <b>$company_name =</b> This is your company name and used throughout the website and in emails.
- <b>$domain_name =</b> Enter your domain name here, do not use "www" here or anywhere else.
- <b>$email_address =</b> Enter the email address you want emails to be sent from.
- <b>$website_color =</b> You can enter a hex code (#000000) here or a color (black).
- <b>$text_color =</b> You can enter a hex code (#FFFFFF) here or a color (white).
- <b>$homepage_text =</b> This is the text that will be used on the website's homepage.
- <b>$payment_text =</b> The text used when requesting payment details (PayPal Email, Bitcoin Address, etc).

These are the percents you share with publishers and affiliates.

- <b>$holding_period =</b> This is the amount of time commissions are pending.  Since DirectRTX pays on a NET-30 basis, we suggest you set this variable to "45".  This will give you 15 days to pay publishers after you receive the payment from DirectRTX.  With "45" set, you'd pay January's earnings on March 15th.
- <b>$publisher_percent =</b> This is the percent of revenue you want to share with publishers.  We suggest sharing 60-80% of revenue.  But you can feel free to set it to whatever you want.
- <b>$affiliate_percent =</b> This is the percent of the publisher's revenue that an affiliate earns.  Normally 10% is used as the industry standard, but once again, feel free to set it to whatever you want.

You will need to create a free account at Google's reCAPTCHA service.  You must select reCAPTCHA v2 and the Checkbox option.  Enter your domain when asked for it during the signup process.  You can enter whatever you want as the title.

- <b>$recaptcha_public =</b> This is where you enter the "Site key" Google provides you.
- <b>$recaptcha_private =</b> This is where you enter the "Secret key" Google provides you.
- <b>$recaptcha_theme =</b> You can enter "light" or "dark" here - depending on your color scheme.

Now go to `http://example.com/install.php` to confirm that everything is properly installed.  If everything is working, you'll see a message letting you know.  If the files aren't in the proper place or the script can't connect to your database, you'll get an error message.  If you get an error message, it should be self-explanatory.

## Automation With Cron Jobs

There is one cron file that must run every day, without fail.  Technically, if it fails, it would be a game ender.  When it runs the next day, it'll catchup all of the stats.  But it's pretty important that it runs every day.

We suggest using <a target="_blank" href="https://cron-job.org">Cron-Job.org</a>.  It tends to be more reliable to server-based cron jobs and logs everything.  Go there and create an account.  During the account creation process, it's very important that you select `UTC` as your timezone.  It's the last option in the timezone selector.  Every file of the script is setup ensure UTC is being used as the timezone.

After creating your account, let's create a cron job with the below settings.

You can enter whatever you want as the `Title`.  For the URL, enter this: `http://example.com/cron.php?secretkey=XXXXX`

You will need replace `example.com` with your domain name.  And replace `XXXXX` with whatever you set the `cronjob_key` variable to in your `config.php` file.  A secret key is set to prevent anyone from running your cron.

Under the Schedule section of the cron job, choose to run it `Every day at 0 : 05`.  Under the Notifications settings, select all all options.  Now just click to create the cron job.  You're done!

## Holy Shit!  It's All Setup!

You are now the proud owner of a fully functioning ad network.  And not just any network.  One that's going to handle an unlimited amount of traffic for you and cost you less than $10/month.  You will literally be able to handle more traffic than some networks that are running hundreds of ad servers.  It doesn't get any better than that.

In the sections below, we're going to teach you about the Member's Area that publishers will be using and the Admin Dashboard which is where you can monitor everything.  And don't worry, we don't have any plans on stopping there.  We're also going to teach you how to start promoting your new network!

## Notes About The Member's Area

The Member's Area is pretty self-explanatory.  You can create a test account to login and play around in it.  

You'll find that it contains almost all of the same features as DirectRTX.  The only features it doesn't have is the ability to use SubIDs or ClickIDs - but that's okay.  Most publishers don't use those features, they are primarily used by ad networks.

One important note that applies to both the Member's Area and Admin Dashboard:  anywhere you see traffic counts is referring to the amount of traffic purchased, not the total amount sent by a publisher.  Any traffic not purchased is sent to the publisher's fallback URL if they're using one or your fallback URL if they aren't using one.

## How To Use The Admin Dashboard

You can access the Admin Dashboard here:

`https://example.com/admin.php?secretkey=XXXXXXXXXX`

Replace `example.com` with your domain and `XXXXXXXXXX` with whatever you set the variable `admin_key` to in your `config.php` file.  This secret key is used to prevent anyone from access your admin dashboard.  However, even if someone gained access to it, there's very little damage they could actually to.  The admin area was mainly designed for monitoring.

The first thing you may notice is the time in the upper right corner.  This is to show you the UTC time since the entire system runs off that timezone - when breaking up daily stats or showing any per-day details.

Understanding how the Admin Dashboard works is extremely important because it allows you to monitor everything that's happening in your network.  So, we will go into great detail explaining each part of it below.

<b>Top Stats Section</b>

There are 12 stats boxes, here's what they mean:

- <b>Active Members -</b> The number of members that have either signed up or sent traffic in the last 24 hours.
- <b>Earning Members -</b> The total number of members that have ever sent traffic to your ad network.
- <b>Total Members -</b> The total amount of members that have created an account in your network at any time.
- <b>Pending Payments -</b> The total amount of payments you need to send out.  Will show $0.00 except on pay day.  
&nbsp;  
- <b>Daily Traffic -</b> The total amount of visitors that have been purchased today (today - not the past 24 hours).
- <b>Daily Profit -</b> The total amount of profit you, as the network owner, have earned today (today - not the past 24 hours).
- <b>Daily Revenue -</b> The total amount of revenue earned by your network today (today - not the past 24 hours).
- <b>Daily CPM Rate -</b> The network's overall CPM rate for today (today - not the past 24 hours).  
&nbsp;  
- <b>Total Traffic -</b> The total amount of visitors that have been purchased in the lifetime of your network.
- <b>Total Profit -</b> The total amount of profit you have earned in the lifetime of your network.
- <b>Total Revenue -</b> The total amount of revenue earned in the lifetime of your network.
- <b>Total CPM Rate -</b> The network's overall CPM rate in the lifetime of your network.

<b>Member's List Section</b>

This section lists all of your members that have ever earned money.  This list only contains a list of members that have sent traffic to your network.  There's a lot of members that signup and never do anything.

Here's a breakdown of each column in this table:

- <b>ID -</b> The publisher's ID number in the database - also, used in their direct link.
- <b>Email -</b> The publisher's login email address - this may be different than their payment email.
- <b>Traffic -</b> The amount of traffic that's been purchased from this publisher.
- <b>CPM Rate -</b> The average CPM rate we're purchasing traffic from this publisher at.
- <b>Revenue -</b> The total amount of revenue this publisher has generated for your network.
- <b>Earnings -</b> The total amount the publisher has earned (including current and paid balances).
- <b>Profit -</b> The total amount of profit you've earned from this publisher in their lifetime.
- <b>Activity -</b> This is the last time we notified your network that traffic has been purchased from this publisher.

<b>Daily Stats Section</b>

This section just shows your network's stats over the past 30 days.  There's nothing really special about it, it's simply there to help you monitor how the network is growing over time.  Your database also stores the stats for every day forever.

- <b>Date -</b> This is the date that the statistics in that row are for (in the UTC timezone).
- <b>Members -</b> The total amount of members that sent traffic to your network on that day.
- <b>Traffic -</b> The total amount of traffic that was purchased from your network on the specified day.
- <b>CPM Rate -</b> The network's average CPM rate (across all members) for that day.
- <b>Revenue -</b> The total amount of revenue generated by your network that day.
- <b>Earnings -</b> The total amount of money your members earned on the specified day.
- <b>Profit -</b> The total amount of profit your network earned on that day.

<b>Hidden Payments Section</b>

Whenever payments are due to someone, a new section will appear that's normally hidden.  It will have a list of any members you need to send payments to along with their payout details and the amount owned.  You'll be able to mark member's as paid after you send each payment.  You will be required to enter a transaction ID for record keeping.  This can be anything from a PayPal transaction ID to a Bitcoin transaction ID to a random string that you've generated.

## Start Promoting Your Network!

Now that your network is setup and you understand how everything works, it's time to start promoting it.  People aren't going to just magically know your network exists.  So, we'll help you get started.  If you follow all of the suggestions in this section, you'll have at least 100 new publishers within 30 days of finishing everything.

First, you need to submit your network to the top blogs that promote new networks.

- <b>ADSWikia - https://adswikia.com/add-network/   
- Adswiki - https://www.adswiki.net/add-network-program  
- Make Money With URL - https://makemoneywithurl.com/submit-ad-network</b>  

These blogs will take days (or weeks) to list your network.  So, let's move on to the next step:

- <b>MyMediAds - https://mymediads.com</b>

MyMediAds is designed specifically for attracting publishers and advertisers.  So, you should be consistently posting advertisements here and bumping your existing ads to the top.  You can also respond to other people's ads, chat with them in Skype, and start networking to grow your network.

And finally, use forums to promote your new network - they are great places to find publishers:

- <b>DigitalPoint - https://forums.digitalpoint.com/forums/pay-per-click-advertising.20/
- Warrior Forum - https://www.warriorforum.com/ad-networks-cpm-cpl-display/
- BlackHatWorld - https://www.blackhatworld.com/forums/pay-per-click.13/
- TheBot.net - https://thebot.net/forums/traffic-cash.153/
- WickedFire - https://www.wickedfire.com/traffic-and-content/
- V7N Forum - http://www.v7n.com/forums/webmaster-revenue/
- Affilorama - https://www.affilorama.com/forum/ppc/
- SEO Chat - http://forums.seochat.com/other-ppc-37/
- BitcoinTalk - https://bitcointalk.org/index.php?board=84.0
- DNForum - https://www.dnforum.com/forums/monetization-of-domain-names.800/
- AffiliateFix - https://www.affiliatefix.com/forums/payperclick/
- Making Money With Android - http://forums.makingmoneywithandroid.com/advertising-networks/
- IMSEOLab - https://www.imseolab.net/Forum-Adult-PPV-PPC-Media-Buying-Mobile-etc
- BlackHatTeam - http://www.blackhatteam.com/forums/pay-per-click-ppc.135/
- CPA Elites - https://www.cpaelites.com/Forum-Main-CPA-Discussions-Elites-Helpdesk
- DreamTeamMoney - http://www.dreamteammoney.com/index.php?showforum=870
- Money Maker Discussion - http://www.moneymakerdiscussion.com/forums/traffic-depot-ppc-ppv-media-buys.325/
- TopGoldForum - https://topgoldforum.com/forum/38-generate-traffic/
- CPA Hero - http://www.cpahero.com/Forum-Not-CPA-PTC-PPC-PPV-PTP-CPM-General-Discussions-Network-Reviews
- Black Hat SEM - https://www.blackhatsem.com/Forum-SEO-Internet-Marketing-Social-Media-Tools-Software-Bots
- Hack Forums - https://hackforums.net/forumdisplay.php?fid=268</b>

Please note that we didn't review the rules of each forum listed above, but as long as you're just telling people about your new network and not being too spammy, most forums owners are pretty cool about it.  In general, you should just create one thread in each forum we linked to above.  And make sure you check it on a daily basis - every time you respond to someone, the thread will bump to the top of the forum - which gets a lot more eyes on it.

Also, don't forget that some forums have a culture where members are very untrusting or just like to troll new users.  So, don't be surprised if you're questioned or come under fire.  Just relax - answer questions and be polite.  For every person that talks shit - there's several more people that just visited your network because they're interested in it.

One of the most important things to remember is what makes your network different.  You can run a general popunder network or you could focus on specific types of traffic.  For example, you could specifically try to attract adult publishers or people selling proxy traffic.  Another great way to differentiate yourself is by offering a unique payment method. For example, you could start a network that exclusively pays out in Ethereum or Monero.  It's completely up to you.

And of course, these are all webmaster or internet marketing forums.  So, you should definitely mention that you have an affiliate program.  Even if someone doesn't want to send traffic, they may be interested in promoting it.

## Important Details About Payouts

One of the top complaints about ad networks is publishers not getting paid out or having their earnings "adjusted" right before it's time to payout.  Sometimes that happens due to chargebacks from advertisers, sometimes that happens because the networks are just scammers.  You don't want to be one of those guys.  They make a little money short term, but they'll never experience how much they could be earning by running a network the right way.

You don't have to worry about getting paid ever.  When DirectRTX sends a postback with revenue details, you're absolutely guaranteed that payment.  So, you have no reason to not pay publishers.

Additionally, you should be so excited to send payouts.  Every time you send a payout, you're reminding the publisher that you exist and you reminding them that you always send payouts on time.  That's one of the most important aspects to growing a network.  The entire reason publishers are sending you traffic is for these payments.

## Words of Encouragement...

Getting an ad network popular isn't as easy as you'd think.  It's absolutely worth it because there's a shitload of money you can make, but that doesn't mean it's easy and there will absolutely be times that you feel like giving up.

When you feel that way, just remember that we've already done all the heavy lifting for you.  You're never going to have to deal with the stress of managing hundreds of servers.  You don't have to worry about chargebacks from advertisers.  You don't even have to worry about your system ever going offline.  We've taken away every stress we possibly can.

We did this so that you can dedicate all of your time to promoting your new ad network.  But if for some reason you decide to shutdown your network.  Send the payouts you owe to publishers and then use your DirectRTX referral link to send them to us.  That way you shutdown your network the right way, but still continue earning from publishers you referred to us :)

Good luck running and promoting your new network - we wish you the best of luck!

— The DirectRTX Team
