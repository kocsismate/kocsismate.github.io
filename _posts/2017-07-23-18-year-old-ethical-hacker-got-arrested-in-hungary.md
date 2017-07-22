---
layout: post
title: "18-year-old ethical hacker got arrested in Hungary"
date: 2017-07-23 20:00:00
categories: security social-justice
tags:
image: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/cover.jpg
---

I am writing this blog post because I haven't found any news in the international media about the recent technology-related
scandal in Hungary, and my intention is to draw attention to the topic, and raise awareness of the importance of security
and proper crisis management when something goes really bad as well as praise the power of the freedom of speech. So let's
see first what have just happened in Hungary!

## Security gone wrong

[T-Systems Hungary][t-systems-hu-website] (which is owned by [Magyar Telekom Nyrt.][telekom-website] which is owned by
[T-Systems][t-systems-de-website]) developed a web application for the public transportation company of Budapest
([BKK Zrt.][bkk-website]) that was opened for the masses on the 14th July.

This application is an online shop of tickets and monthly Budapest-passes. The digital tickets you buy from here can be
shown on your smart phones to the ticket controller personnel until the fully electronic ticket system ([RIGO][rigo-website])
is deployed in Budapest (this is expected at the end of 2018). This is great news, and I feel that we are finally
reaching the technology level of the 21st century!

![BKK Online shop][bkk-app]

What's the catch then? Unfortunately, the devil is in the details, so during the first week of operation, many-many
severe security vulnerabilities and usability problems have been found. Here they are without the need for completeness:

- The SSL connection of the site got the worst, "F" rate on [SSL Labs][bkk-ssl-report]
!["F" rate on SSL Labs][bkk-ssl]
- The CAPTCHA on the registration form is [ridiculous][bkk-captcha-twitter]
![So called "CAPTCHA" protection][bkk-captcha]
- Your email address didn't have to be verified so you could spam anybody you want
- Your password used to be sent out directly in unencrypted mail if you had forgotten your password
- Password fields used to be filled out when editing your personal details
- You used to be able to get access to personal details (including the password) of other registered users with limited
IT knowledge
- As there is currently no possibility to delete your account on the website itself, you can ask the IT Support to do so,
and they were willing to perform the action without any verification, even though you wrote them from a different email
address from the one you had registered with
- You could modify the price of the ticket by changing the value of the price input field on the checkout page which shows
that the price wasn't validated properly on the server-side so this monthly Budapest-pass could be bought by 50 HUF instead
of 9 500 HUF (roughly 30 EUR):
![A monthly Budapest-pass bought by 50 HUF instead of 9 500 HUF (roughly 30 EUR)][bkk-ticket]
- You can fake the digital ticket so that you can easily pass the validation at the ticket controllers because very few
of them have QR code readers.

All in all, this website is a complete parody of information security, a real counterexample of responsible data handling.
This level of negligence just isn't acceptable in 2017 when half of our life is online. Moreover, tens of thousands
of people could possibly use this website so the impact of its security is rather big.

But this isn't the worst part of the story. The real horror will just come!

## Crisis management gone wrong

T-Systems Hungary - the developer of the application - denied that any security vulnerability has been exploited:

> There's no evidence of that anybody's password or personal data would have been compromised

said Mr. Kálmán Dabóczi, CEO of BKK Zrt. (the above text is a paraphrase). However, he admitted that there were several
attacks and trolling attempts against the website. Mr. Balázs Szeneczey, vice mayor of Budapest announced that
T-System Hungary Zrt. has already reported an attacker to the police.

Then it came out that the aforementioned "attacker" is a 18-year-old kid almost without any computer education who
discovered that tickets can be bought [for any price you want](#security-gone-wrong) and who **immediately** reported this
bug to the public transportation company. The next day, this young guy was **arrested by the police early in
the morning**.

Later that day, BKK Zrt. and T-Systems Zrt. made a common announcement in which they stated that "the developer company had
to report the event 'which reached a certain level' to the police because of a strict internal policy." They added that
"they were very sad to hear that the suspect is such a young student who seemed to have good intentions based on his
interviews in the media".

This is just insane. Arresting an ethical hacker for helping a company out? I'll write more about this topic a bit later,
but let's just continue the original story with the fun part!

## People gone mad

The news about arresting the young ethical hacker drove people crazy and a mass mysteria soon broke out throughout Hungary.
People wanted to take revenge on BKK and T-Systems, so they started to rate these companies on Facebook. Yesterday at 3 p.m.
there were more than 1500 one-star ratings on the [official Facebook page of BKK][bkk-facebook], most of them also
blaming the two companies for their unprofessional attitude in the added comments. At the time of writing (22nd July at 10 p.m)
this number increased up to **44 000 one stars**, while the [official Facebook page of the German T-Systems][t-systems-de-facebook] 
received more than 5000 one stars (unfortunately [the Hungarian page][t-systems-hu-facebook] can't be rated)!

![44K one-star ratings!][bkk-rating]

Furthermore, probably real hackers were also enraged so they supposedly made the [website of BKK][bkk-website]
unavailable for an extensive period of time by continuous (D)DoS attacks. In the meanwhile, people started to create
memes from the incident thus further mocking and shaming these companies. You can find [a classic one][bkk-meme1-facebook]
below:

!["Fucking hackers!"][bkk-meme1]

> Fucking hackers!

But my personal favourite is [this one][bkk-meme2-facebook]:

![Grade "F" for the marketing division of BKK"!][bkk-meme2]

> - Mr. Teacher, I didn't study, please give me grade "F"!
> - Will be 17 000 pieces of it enough?

Background: the worst grade one can receive in Hungary is "1", while the best one is "5".

## City mayor gone mad

Mr. István Tarlós, City Mayor of Budapest was surely informed about the rebellion on the internet, so he ordered
immediate investigation. And you won't believe what happened next! Mr. Kálmán Dabóczi, CEO of BKK publicly apologized
about the problems around the new application and requested an incident report from T-Systems Hungary. It is even
more ironic what Mr. Zoltán Kaszás, CEO of T-Systems Hungary wrote afterwards:

> It is indisputable that there are more modern and more advanced solutions out there for certain components of the
system.

Then he continued:

> As the leader of T-System Hungary, in case of his ethical behaviour gets proven, I would like to offer him the
possibility to work together if he is open to it.

He also promised to set up a bug bounty program, like most of the [better companies][github-bounty].

## Conclusion

So what is to be learnt here?

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
[t-systems-de-website]: https://www.t-systems.com
[t-systems-de-facebook]: https://www.facebook.com/tsystems/
[telekom-website]: https://www.telekom.hu
[index-bkk-tag]: http://index.hu/24ora/?cimke=bkk+e-jegy
[github-bounty]: https://bounty.github.com

[bkk-app]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-app.jpg
[bkk-ssl]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-ssl.jpg
[bkk-captcha]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-captcha.jpg
[bkk-ticket]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-ticket.jpg
[bkk-rating]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-rating.jpg
[bkk-meme1]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-meme1.jpg
[bkk-meme2]: /assets/image/2017-07-23-18-year-old-ethical-hacker-got-arrested-in-hungary/bkk-meme2.jpg
