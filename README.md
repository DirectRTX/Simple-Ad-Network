# Simple Traffic Network
Simple Traffic Network is a free, open source PHP script to start your own traffic network.  This script is designed by the team at DirectRTX to allow anyone to start their own popunder network or media buying system.

Our #1 goal when developing this script was to allow anyone to start their own network for less than $10/month and make sure they never have to spend more than that until they're earning at least $5,000/day.  Seriously, you should be making at least $5000/day before you have to invest more than $10/month for hosting.

Please read the full documentation before setting up your own network.  If you've ever installed a script like WordPress - this will be just as easy.  But there's a lot of moving parts to make sure that your network can easily handle hundreds of millions of hits per day.  Below we'll walk you through every step of getting setup and explain how everything works.

By the way, this is one badass system.  It can handle unlimited traffic, has a built-in affiliate program, and provides publishers with multiple ways (popunders, direct links, etc) to send traffic.  There's nothing else like it online.

## How You'll Make Money
We know that's what you're here for, so let's get right to it.

Your ad network will be able to handle an unlimited amount of publishers.  All of the traffic is going to be routed using CloudFlare, so the traffic itself never even hits your server.  Managing multiple clusters of servers handling hundreds of millions of hits per day can be a huge task - we've handled that for you.

First the traffic will be sent to DirectRTX.  The automatic postback system at DirectRTX will automatically ping your system whenever traffic is purchased and your system will automatically credit it to the correct publisher's account.  So, you'll make money by paying a percent of that money to publishers and keeping a percent for yourself.

Additionally, you'll have options to monetize the traffic that DirectRTX doesn't purchase - which is where you can make a ton of money.  We'll get more into those details later on in the documentation.  Don't worry, this is all about making money :)

Oh, and at the end of this, we're even going to teach you how to promote the network.

## What You Need to Get Started
Please make sure you have the following things before you get started:

1.  A domain name.  We recommend using <a href="https://www.namesilo.com">NameSilo</a>.
2.  A web hosting account.  We recommend <a href="https://www.stablehost.com">StableHost</a>.
3.  A free account at <a href="https://www.cloudflare.com">CloudFlare</a>.  No upgrades needed.
4.  An account at <a href="https://directrtx.com">DirectRTX</a>.  Instantly approved.
5.  A <a href="https://www.paypal.com/">PayPal</a> account.  Used for payments from DirectRTX.

You can use any web hosting company you want, but make sure this script is the only thing installed in the account.  It was developed using StableHost so we know it works perfectly there.  Just make sure that whatever hosting company you use has PHP and MySQL (or MariaDB) available - also, it needs to run on Apache if possible.

So, let's get started setting up everything below.  We'll use our suggestions as examples, but feel free to use whatever domain registrar and hosting company that you want.

### Register Your Domain Name

Your domain name is your brand, but we shouldn't have to teach you that.  Look at some of the names of other popunder networks and come up with something unique.  Once you've found a good domain name, register it at NameSilo.
