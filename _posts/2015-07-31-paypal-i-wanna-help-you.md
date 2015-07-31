---
layout: post
title:  "PayPal, I just wanna help you!"
date:   2015-07-31 16:18:00
categories: personal
---

Long story short, PayPal's new webpage has a pretty annoying bug which I wasn't
able to properly report but I needed to work around. Even worse, their customer
service failed to handle this issue despite I filled in a detailed bug report
with screenshot and possible solution. Heads up, AJAX POSTing and
firebug is coming to your rescue if you want to use PayPal!

### Why PayPal?

PayPal is great! I love their service and it already made my life easier
multiple times when it came to online shopping. In the last couple of days tho,
I had an embarrassingly simple problem which I couldn't even explain the
customer support, I guess. What's my issue? I wanted to add an bank account
number to my PayPal account, in order to transfer money to it.

### Trouble with customer service

During the last weeks I experienced PayPal's customer service's suboptimal
workflow. After reporting my issue, I got a nicely worded email where they
promised to contact me within 24 hours. Wow, that's sweet! - what I thought. It
was indeed sweet until I needed to reply that mail. The message is sent from
webform@paypal.com - this basically means that whoever contacted you, you can't
be sure that your reply will go to the same person. 

And this happened to me. After several replies I ended up getting emails from
four different persons who all were really nice and started asking what my
problem is and how they can help.

The more annoying part is that some of these very nice customer service
employees didn't even get the point. And sometimes it's just so hard to stay
polite and constructive.

They claim they tried to contact me however I never got any phone calls. It
could be a technical issue of course (I double checked my phone number). What
makes me angry about this, that they never replied to the original issue
(software bug) at all. They also asked me to send a copy of my ID with a picture
and a bank account statement and they will add the number manually. WOW.

And what makes you the most miserable about all this thing: after each mail you
send you need to wait a whole day due their 24 hour response policy.

PayPal, this is far from optimal. I'd suggest to review your customer service
policy and processes, because it makes both peers miserable.

### The bug: cannot add bank account number if it contains a letter

And swiss account numbers sometimes do. Let's have a look on my Banks info page
about how a UBS bank account number builds up. These screenshots are the same as
what I sent to the customer service.

![UBS account number](/blog/img/2015-07-31/01.png)

I have a similar account number, so I tried to add it on their webpage:

![PayPal bank account wizard](/blog/img/2015-07-31/02.png)

The error message says in German: "Only letters are allowed, no whitespaces or
dashes". Well, this clearly is a verification error. This is a Swiss PayPal
account, thus I'd expect that a Swiss bank account number can be added. After my
week-long struggle with the customer service, I decided to find out whether it's
a client-side error only or not.

Now comes the technical part.

I tried to give in a dummy account number, `1111 1111 1111`. It worked! I got a
`200 OK` HTTP status code back. Good. Now let's try rewriting the POST workload
manually:

![Firebug showing the POST message](/blog/img/2015-07-31/03.png)

Should it work...? Meeeh, it mustn't, for sure. THey must have the same
validation both on client and server side.

![Workaround was successful](/blog/img/2015-07-31/04.png)

WOW. On the contrary, it worked! This is kind of a
throw-out-the-junior-if-doesn't-validate-on-booth-side type of error, but you
know, we are just people, we tend to make errors, who cares.

### Please, accept my bug report!

So now If I look at my Paypal home page, I can see that the account has been
successfully added:

![Paypal home page](/blog/img/2015-07-31/05.png)

I sincerely hope that my message will get to a developer or a manager at your
software department. Here it is:

> PayPal, it looks like you have a small bug in your client side input validation
> settings. Unfortunately I could not get through your customer service, but
> hope that you will be notified about this issue, so you can fix it. Until this
> error exists, UBS account number holders in Switzerland might not be able to
> add their bank account to PayPal thus they can't transfer money to it. 

Let's hope they fix the issue and I don't get kicked out for tampering with the
POST messages in my browser ;-)

