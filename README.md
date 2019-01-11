# Simple Traffic Network
Simple Traffic Network is a free, open source PHP script to start your own traffic network.  This script is designed by the team at DirectRTX to allow anyone to start their own popunder network or media buying system.

Our #1 goal when developing this script was to allow anyone to start their own network for less than $10/month and make sure they never have to spend more than that until they're earning at least $5,000/day.  Seriously, you should be making at least $5000/day before you have to invest more than $10/month for hosting.

Please read the full documentation before setting up your own network.  If you've ever installed a script like WordPress - this will be just as easy.  But there's a lot of moving parts to make sure that your network can easily handle hundreds of millions of hits per day.  Below we'll walk you through every step of getting setup and explain how everything works.

This documentation is pretty long.  But - you can actually get your entire network fully setup and running in less than 60 minutes by following these instructions.  Don't believe us?  Time it.  Seriously, it'll be done within 60 minutes.

By the way, this is one badass system.  It can handle unlimited traffic, has a built-in affiliate program, and provides publishers with multiple ways (popunders, direct links, etc) to send traffic.  There's nothing else like it online.

## How You'll Make Money
We know that's what you're here for, so let's get right to it.

Your ad network will be able to handle an unlimited amount of publishers.  All of the traffic is going to be routed using CloudFlare, so the traffic itself never even hits your server.  Managing multiple clusters of servers handling hundreds of millions of hits per day can be a huge task - we've handled that for you.

First the traffic will be sent to DirectRTX.  The automatic postback system at DirectRTX will automatically ping your system whenever traffic is purchased and your system will automatically credit it to the correct publisher's account.  So, you'll make money by paying a percent of that money to publishers and keeping a percent for yourself.

Additionally, you'll have options to monetize the traffic that DirectRTX doesn't purchase - which is where you can make a ton of money.  If a publisher doesn't set a fallback URL (around half of them tend not to), you'll be able to set a default URL where all that unsold traffic gets sent to.  Any money you earn from these networks will be 100% profit for you - most networks don't have features like DirectRTX, so there's no way to credit that money to publishers.

Before you start assuming this is shady - remember, this tends to be standard practice in the popunder world - espcially when publishers are given the chance to set their own fallback URL.  If a network doesn't have direct advertisers for traffic, they just sell it off to other networks and keep the profit.  Don't worry, this is all about making money :)

Oh, and at the end of this, we're even going to teach you how to promote the network.

## What You Need to Get Started
Please make sure you have the following things before you get started:

1.  A domain name.  We recommend using <a href="https://www.namesilo.com">NameSilo</a>.
2.  A web hosting account.  We recommend <a href="https://www.stablehost.com">StableHost</a>.
3.  An account at <a href="https://directrtx.com">DirectRTX</a>.  Instantly approved.
4.  A free account at <a href="https://www.cloudflare.com">CloudFlare</a>.  No upgrades needed.
5.  A <a href="https://www.paypal.com/">PayPal</a> account.  Used for payments from DirectRTX.

You can use any web hosting company you want, but make sure this script is the only thing installed in the account.  It was developed using StableHost so we know it works perfectly there.  Just make sure that whatever hosting company you use has PHP and MySQL (or MariaDB) available - also, it needs to run on Apache if possible.

So, let's get started setting up everything below.  We'll use our suggestions as examples, but feel free to use whatever domain registrar and hosting company that you want.

### Register Your Domain Name

Your domain name is your brand, but we shouldn't have to teach you that.  Look at some of the names of other popunder networks and come up with something unique.  Once you've found a good domain name, register it at NameSilo.

Please don't email asking for suggestions, we don't care what you name your network.

### Create A Web Hosting Account

Go to StableHost and signup for the cheapest plan.  After creating your account, they will provide you with your nameservers.  Nameservers are used to point a domain name to the server it's hosted.  So, go back to the company you registered your domain name with and change the nameservers for your domain to the ones provided by StableHost.

### Signup at DirectRTX.com

Go to DirectRTX.com and create an account.  It's simple and doesn't even require email verification.

Once you've created your account, you'll need to login and do 2 things.  Make sure you pay attention here:

1.  Go to the "My Links" section and you'll see your unique link.  In that link is a 6 digit number - write it down.
2.  Go to https://directrtx.com/postback-settings.php and enter the following URL:

```http://example.com/postback.php?revenue=[revenue]&clickid=[clickid]&secretkey=XXXXXXXXXX```

Replace `example.com` with your domain name (without www).  Replace with `XXXXXXXXXX` with a unique 15-digit code.  You can use <a href="https://passwordsgenerator.net/">PasswordGenerator.net</a> to generate this code - just make sure it's only letters and numbers, no special characters.  The unique code is to make sure nobody can send fake postbacks to credit their account.  Do'nt share it with anyone.

### Getting Setup At CloudFlare

This is the most complicate step you'll perform during the setup process - that should tell you this who process is going to be pretty damn easy.  Remember, CloudFlare and DirectRTX are the reason you'll be able to handle hundreds of millions of hits on a daily basis, so it has to be setup correctly.  So, let's get started:

1.  Go to CloudFlare.com and register an account.

2.  During the registration process, you'll need to add your domain.

3.  For your domain to be activated, you'll need to change the nameservers at your domain registrar (again) to point to the ones CloudFlare provides you with.  We first pointed them to your hosting company so CloudFlare can grab the correct DNS records and automatically point to your domain to your hosting company as well.

Once you've completed the 3 steps above, your account and domain are setup at CloudFlare.  But it doesn't end there.  To make the magic happen, we'll need to do 2 more things:  create a couple of CNAME records and setup Page Rules.

<b>How to Create CNAME Records</b>

Select your domain and go to the "DNS" tab in CloudFlare's dashboard.

Each record you add has the option select or enter 4 fields.  Add these two records:

`CNAME` `go` `x.directrtx.com` `Automatic TTL`

`CNAME` `traffic` `x.directrtx.com` `Automatic TTL`

After these are added, make sure there's an orange cloud next to each of them.

You're done setting up the required DNS records.  It really wasn't that difficult was it?

<b>How to Create Page Rules</b>

Go to the Page Rules tab in CloudFlare's dashboard.

You're going to create 3 pages - all of them are going to use the `Forwarding URL` setting.  Also, they will all use the `Status Code` 301. Now that you know those 2 settings are used by all 3 page rules, create these:

<b>URL Match Line #1:</b> `*go.example.com/*/?fb=*`  
<b>Destination URL #1:</b>  `http://traffic.example.com/?subid=[DIRECTRTX-ID]&clickid=$2&fb=$3`

<b>URL Match Line #2:</b> `*go.example.com/*/*`  
<b>Destination URL #2:</b>  `http://traffic.example.com/?subid=[DIRECTRTX-ID]&clickid=$2&fb=[FALLBACK-URL]`

<b>URL Match Line #3:</b> `*go.example.com*`  
<b>Destination URL #3:</b>  `http://traffic.example.com/?subid=[DIRECTRTX-ID]&fb=[FALLBACK-URL]`

Here's a description of what each Page Rule is doing:

<b>Page Rule #1 -</b> Passes along your publisher's Fallback URL whenever they've entered one.  
<b>Page Rule #2 -</b> Automatically enters your Fallback URL whenever a publisher doesn't set their own.  
<b>Page Rule #3 -</b> Catches all traffic that doesn't include a publisher's ID number and redirects it.

You will need to replace these three things in each of the rules above (while you're adding them):

`example.com` - Replace this with your own domain name.  Leave the `go.` and `traffic.` parts alone.  
`[DIRECTRTX-ID]` - Replace this with your 6-digit ID number that you got earlier from DirectRTX's dashboard.  
`[FALLBACK-URL]` - Replace this with YOUR fallback URL - where you want unsold traffic to go to.

We're going to talk more about the Fallback URL in the next section.  Please read it carefully.

But you're done setting up CloudFlare at this point!  Woohoo!

<b>Using A Default Fallback URL</b>

First and foremost, your Fallback URL should be URL Encoded.  So, after you choose what you want your Fallback URL to be, go to <a href="https://www.urlencoder.org/">URL Encoder</a> and encode it.  The encoded version is what needs to be used in your Page Rules.

For your Fallback URL, you have 4 options to choose from (from simplest to most complicate):

1.  <b>Set it as your ad network's homepage.</b>  Any unsold traffic will be sent there and advertise your network.  You won't earn money directly from this traffic, but some people may signup and earn money for you.

2.  <b>Send the traffic to a single network.</b>  There are plenty of networks like PopCash, Propeller Ads, and ZeroPark that will provide you with a direct link that you can send the unsold traffic to and make money.

3.  <b>Send the traffic to <a href="https://www.adspyglass.com/">AdSpyGlass</a>.</b>  This is an ad mediation network that will automatically forward your traffic to the network its algorithm detects will pay the most for that specific visitor.  It will also send unsold traffic from one network to the next using a waterfall system (described below).

4.  <b>Setup your own waterfall system.</b>  You can signup for multiple networks that provide both direct links and fallback URLs.  For example, you can set Network #1's fallback URL as the direct link from Network #2 and set the fallback URL for Network #2 as the fallback URL from Network #3 and so on.  But in our opinion, it's easier to just use AdSpyGlass to handle all of that for you - they are free and take 10% of your traffic for using their service.

How you choose to handle unsold traffic is completely up to you.  You may be able to find more unique ways to monetize it and that's totally your decision.  These are just the most popular methods people use.
