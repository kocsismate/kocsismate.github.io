---
layout: post
title: "18-year-old ethical hacker got arrested in Hungary"
date: 2017-07-23 20:00:00
categories: security
tags: social-justice
image: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/cover.jpg
---

I am writing this blog post because I haven't found any news in the international media about the recent technology-related
scandal in Hungary, and I want to draw attention to the topic while raising awareness of the importance of information
security and proper crisis management as well as praising the power of social networks. So let's see first what kind
of craziness has just happened in Hungary!

## Security gone wrong

[T-Systems Hungary][t-systems-hu-website] (which is owned by [Magyar Telekom Nyrt.][telekom-website] which is owned by
[Deutsche Telekom AG][deutsche-telekom-website]) developed an online shop for tickets and monthly passes for the public
transportation company of Budapest ([BKK Zrt.][bkk-website]) that was made available for the masses on 14th July.

![BKK Online shop][bkk-app]

The digital tickets you buy from the webshop can be presented on your smart phone to the ticket controller personnel
until the fully electronic ticket system ([RIGO][rigo-website]) is deployed in the capital (it is expected at the end of
2018). This is great news and I feel that we are finally reaching the technology level of the 21st century!

Unfortunately the devil is in the details, so during the first week of operation many-many severe security vulnerabilities
and usability problems have been discovered. Here they are without the need for completeness:

- The SSL connection of the site got the worst, "F" rate on [SSL Labs][bkk-ssl-report]
!["F" rate on SSL Labs][bkk-ssl] (the report might not be available now because SSL Labs was apparently blocked from
accessing the webshop)
- The CAPTCHA on the registration form is [ridiculous][bkk-captcha-twitter]
![So called "CAPTCHA" protection][bkk-captcha]
- Email addresses weren't verified which allowed potential abuse
- Your password used to be sent out directly in unencrypted mail when you requested a password reminder
- Password fields used to be filled out when editing your personal details
- One used to be able to get access to personal details (including the password) of other registered users with limited
IT knowledge by using an older web browser
- As there is currently no possibility to delete your account on the website itself, you can ask the IT Support to do so,
and they were willing to perform the action without any verification, even though you wrote them from a different email
address from the one you had registered with
- You could modify the price of the ticket by changing the value of an input field on the checkout page which clearly
indicates that the price wasn't validated properly on the server-side. That's why the following monthly Budapest-pass
could be bought for 50 HUF (~ 0.15 EUR) instead of 9 500 HUF (roughly 30 EUR):
![A monthly Budapest-pass bought for 50 HUF instead of 9 500 HUF (roughly 30 EUR)][bkk-ticket]
- Icing on the cake is that only a very few of the ticket controllers have QR code readers so they can be bypassed
easily using fake tickets

All in all, this website is a complete parody of information security, a real counterexample of responsible data handling.
This level of negligence just isn't acceptable in 2017 when half of our life is online. Moreover, tens of thousands
of people could possibly use the application so the impact of its security is rather big.

But this isn't the worst part of the story. The real horror will just come!

## Crisis management gone wrong

BKK Zrt. denied that any security vulnerability has been exploited:

> There's no evidence that anybody's password or personal data would have been compromised

said Mr. Kálmán Dabóczi, CEO of the company (the above text is a paraphrase). However, he admitted that there were several
(cyber)attacks and trolling attempts against the website. Mr. Balázs Szeneczey, vice mayor of Budapest announced that
T-System Hungary Zrt. has already reported an attacker to the police.

Then it came out that the aforementioned "attacker" is a 18-year-old kid almost without any computer education. He was
the one who discovered that tickets can be bought [for any price you want](#security-gone-wrong) and who **immediately**
reported the bug to the public transportation company. The next day, the young "hacker" was **arrested by the police early in
the morning**.

Later that day, BKK Zrt. and T-Systems Zrt. made a common announcement in which they stated that

> The event "which reached a certain level" had to be reported to the police because of a strict internal
policy of the developer company.

They added that it is very sad to hear that the suspect is such a young student who seemed to have good intentions
based on his interviews in the media.

This is just insane. Arresting an ethical hacker for helping a company out? I'll write more about this topic a bit later,
but let's just continue the original story with the fun part!

## People gone mad

The arrest of the young ethical hacker hit the news immediately and a mass hysteria soon broke out throughout Hungary.
People wanted to take revenge on BKK and T-Systems so they started to rate these companies on Facebook. There were more
than 1500 one-star ratings on the [official Facebook page of BKK][bkk-facebook] yesterday at 3 p.m., most of them also
blaming the two companies for their unprofessional attitude in the added comments. At the time of writing (22nd July at 10 p.m)
this number increased up to **44 000 one stars**, while the [official Facebook page of the German T-Systems][t-systems-de-facebook] 
received more than 5000 one stars (unfortunately they have nothing to do with [the Hungarian company][t-systems-hu-facebook])!

![44K one-star ratings!][bkk-rating]

Probably real hackers were also enraged so they supposedly made the [website of BKK][bkk-website]
unavailable for an extensive period of time by continuous (D)DoS attacks. Meanwhile, people started to create
memes from the incident to mock and shame these companies. You can find [a classic one][bkk-meme1-facebook]
below:

!["Fucking hackers!"][bkk-meme1]

> Fucking hackers!

But my personal favourite is [this one][bkk-meme2-facebook]:

![Grade "F" for the marketing division of BKK"!][bkk-meme2]

>- Mr. Teacher, I didn't study, please give me grade "F"!
>- Will be 17 000 pieces of it enough?

Background: the worst grade one can receive in Hungary is 1, while the best one is 5.

## City mayor gone mad

Mr. István Tarlós, City Mayor of Budapest was surely informed about the rebellion on the internet and he ordered the
immediate investigation of the case. And you won't believe what happened next! Mr. Kálmán Dabóczi, CEO of BKK publicly
apologized about the problems around the new application and requested an incident report from T-Systems Hungary. It is
even more ironic what Mr. Zoltán Kaszás, CEO of T-Systems Hungary wrote afterwards:

> It is indisputable that there are more modern and more advanced solutions out there for certain components of the
system.

Then he continued:

> As the leader of T-System Hungary, in case of his ethical behaviour gets proven, I would like to offer him the
possibility to work together if he is open to it.

He also promised to set up a bug bounty program, like most of the [better companies do][github-bounty].

Although the story isn't finished yet, it is likely that it will have happy-ending: security holes in the application
will be fixed, our young ethical hacker will get kind rewards ([Green Fox Academy][greenfox-website] has already
[offered him scholarship][greenfox-facebook]), people responsible for his arrest will probably get some kind of prosecution,
while BKK and T-Systems have already been suited on court because of misusing of personal data.

## Conclusion

So what is to be learnt from the story?

First of all, never ever try to spare resources on fundamental security. It will cost much more money in the end if you
screw up. In my opinion it is evident for lots of companies by now. The main problem I see however is that
many organizations are usually uninterested in fixing long-standing security vulnerabilities because they are either in
a rush for money (thus preferring to develop new features), or don't see much added value of fixing something "that has
been working well for ages" or just have no idea what the problem is.

To be honest, I don't believe T-Systems Hungary wanted to save a little bit of money on development. It's much more
likely that their developers were simply not aware of the "state of the art" in security practices, although there are
so many great materials about the topic (please let me recommend you my favourite sources: [Troy Hunt's][troy-hunt-blog],
[Scott Helme's][scott-helme-blog] and the [Paragon Initiative Enterprises'][paragonie-blog] blog).

This case also confirms my point of view that software development should be regulated as thorougly as other engineering
professions. Our industry should set its standards to a much higher level in security, reliability and code quality than
it currently does. It's because from day to day, our life is affected by software more and more. Fortunately, the progress
we have been seeing in the last decades is really promising, but we still have a long way to go.

Another moral of the story is that if something goes really bad, be brave and take responsibility. This should be quite
natural for everybody, but apparently there are some people who just can't do it. The point is that if you screw up,
you still have one very last chance: to stand up, be honest and apologize for your mistake.

People are usually very understanding because many of them can imagine themselves being in the same situation as you.
Let's take as a great example when a GitLab employee [accidentally deleted their production database][gitlab-incident].
This incident was also extremely embarrassing but they communicated everything so openly (they streamed the resolution
on Twitter, wrote a very nice [postmortem][gitlab-postmortem] and tried to convince us that they do everything in
order to prevent to commit this mistake again) so they actually gained the sympathy of people, and finally many of them
said **thank you** to GitLab for being so open.

The last thing I'd like to highlight is the power of Facebook. It is really fascinating to experience that it is not only
suitable for spreading "fake news", but it can actually force people to back off from constant lying. I am certain
that BKK and T-Systems would have never asked for apology if people hadn't started war on the internet. Although it's
really sad that the fear from the online fury was their main motivator to admit the issues with their system.

## Media coverage

You can read the full story [here][index-bkk-tag] (unfortunately all the articles are in Hungarian).

[bkk-website]: https://bkk.hu/
[bkk-facebook]: https://www.facebook.com/bkkbudapest/
[bkk-captcha-twitter]: https://twitter.com/vista_df/status/885797914437705729
[bkk-ssl-report]: https://www.ssllabs.com/ssltest/analyze.html?d=shop.bkk.hu
[bkk-meme1-facebook]: https://www.facebook.com/bkkmemes/photos/a.398918943784228.1073741827.398912580451531/516520218690766/
[bkk-meme2-facebook]: https://www.facebook.com/tibiatya/photos/a.191488314324804.47864.185770441563258/1115162175290742/
[rigo-website]: https://rigo.bkk.hu/
[t-systems-hu-website]: https://www.t-systems.hu/
[t-systems-hu-facebook]: https://www.facebook.com/tsystemshungary/
[deutsche-telekom-website]: https://www.telekom.com
[t-systems-de-facebook]: https://www.facebook.com/tsystems/
[telekom-website]: https://www.telekom.hu
[index-bkk-tag]: http://index.hu/24ora/?cimke=bkk+e-jegy
[github-bounty]: https://bounty.github.com
[greenfox-website]: https://www.en.greenfoxacademy.com/
[greenfox-facebook]: https://www.facebook.com/greenfoxacademy/posts/2035341296693791
[gitlab-incident]: https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/
[gitlab-postmortem]: https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31/
[troy-hunt-blog]: https://troyhunt.com
[scott-helme-blog]: https://scotthelme.co.uk/
[paragonie-blog]: https://paragonie.com/blog

[bkk-app]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-app.jpg
[bkk-ssl]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-ssl.jpg
[bkk-captcha]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-captcha.jpg
[bkk-ticket]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-ticket.jpg
[bkk-rating]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-rating.jpg
[bkk-meme1]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-meme1.jpg
[bkk-meme2]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-meme2.jpg
