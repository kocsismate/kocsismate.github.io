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
security and proper crisis management as well as praising the power of social networks. So let's see first what have just
happened in Hungary!

## Security gone wrong

[T-Systems Hungary][t-systems-hu-website] (which is owned by [Magyar Telekom Nyrt.][telekom-website] which is owned by
[Deutsche Telekom][deutsche-telekom-website]) developed an online shop for tickets and monthly passes for the public
transportation company of Budapest ([BKK Zrt.][bkk-website]) that was made available for the masses on 14th July.

![BKK Online shop][bkk-app]

The digital tickets you buy from the webshop can be presented on your smart phone to the ticket controller personnel
until the fully electronic ticket system ([RIGO][rigo-website]) is deployed in Budapest (it is expected at the end of 2018).
This is great news and I feel that we are finally reaching the technology level of the 21st century!

Unfortunately the devil is in the details, so during the first week of operation many-many severe security vulnerabilities
and usability problems have been discovered. Here they are without the need for completeness:

- The SSL connection of the site got the worst, "F" rate on [SSL Labs][bkk-ssl-report]
!["F" rate on SSL Labs][bkk-ssl]
- The CAPTCHA on the registration form is [ridiculous][bkk-captcha-twitter]
![So called "CAPTCHA" protection][bkk-captcha]
- Email addresses weren't verified which allowed potential abuse
- Your password used to be sent out directly in unencrypted mail if you requested a password reminder
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
- Icing on the cake is that only a very few of the ticket controllers have QR code readers so they can basically be
bypassed using fake tickets

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

Although the story isn't finished yet, it is likely that it will have happy-ending: security holes of the application
will be fixed, our young ethical hacker will get kind rewards ([Green Fox Academy][greenfox-website] have already
[offered him scholarship][greenfox-facebook]), maybe people responsible for the arrest will get some kind of prosecution.

## Conclusion

So what is to be learnt from the story?

First, never ever spare time and money on fundamental security. ...

Then if something yet goes bad, be brave ...

Furthermore, it is astonishing to see the power of social networks.

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

[bkk-app]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-app.jpg
[bkk-ssl]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-ssl.jpg
[bkk-captcha]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-captcha.jpg
[bkk-ticket]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-ticket.jpg
[bkk-rating]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-rating.jpg
[bkk-meme1]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-meme1.jpg
[bkk-meme2]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-meme2.jpg
