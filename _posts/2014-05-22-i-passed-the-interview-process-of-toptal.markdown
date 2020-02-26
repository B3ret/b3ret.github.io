---
layout: post
date: 2014-05-22
title: I passed the interview process of toptal.com
categories: meta
tags: [C#, Visual Studio]
---

A few days ago I passed the last interview round for
[toptal.com](https://www.toptal.com/#pick-just-supreme-devs) (affiliated). Toptal is a
platform for connecting freelancing software developers with companies. In this sense it
is much like [freelancer.com](https://www.freelancer.com/]) or
[upwork.com](https://www.upwork.com/), but there is one very big difference: they only
accept developers that are actually good.

<!--more-->

{% include vimeo.html id='45519288' %}

### Interview process

Their interview process spans four rounds, takes approximately one month, is well thought
out, and in my opinion very effective:

1. Round one: Skype interview to explain the company, ask about my experience, and explain
   the remaining interview process. They probably asses the ability to communicate
   effectively in English in this step.

2. Round two: Online coding exercise on [codility.com](http://www.codility.com/). This one
   is quite tough, they gave me three tasks with increasing complexity to solve in 90
   minutes. All the tasks are *real* programming riddles. You have to choose good data
   structures, develop intelligent algorithms, and even meet a run time constraint (which
   is given in Big-O-Notation). However, they explicitly state that it is better to
   complete two tasks correctly than to complete all three somewhat correctly. I therefore
   opted for making the first two task *perfect* with good test case coverage and see
   about the last one afterwards. I completed the first exercise in 15 minutes and the
   second one in 60 minutes. Finally, 15 minutes was definitely too short for completing
   task three, so I just wrote a comment about my solution strategy. (After the test, I
   almost programmed the solution for task three, because it was actually a very
   interesting problem...). Feedback came back a few days later by my interviewer as “very
   good”. I solved task one and two perfectly and was scheduled for round three.

3. Round three: Life coding exercise. Two programming tasks were to be solved in a total
   of 60 minutes, but this time the interviewer was watching my progress live via Skype
   screen sharing. The interview started with a review of my solutions for round two. I
   also explained my solution strategy for task three. The first life coding exercise was
   a simple string manipulation task; however, I did rather badly. I’m not used to do low
   level string processing in C# and my solution was correct, but unnecessarily complex.
   The second coding exercise was closer to a real life application, and I solved it fast
   and elegantly. The interviewer congratulated me and I was scheduled for round four.

4. Round four: Real life project. After round three I was given two weeks of time to
   finish a real world project involving a database back-end, a RESTful API, and an AJAX
   front end. Experienced web developers would probably finish this project in a few
   hours, but I took the opportunity to learn more about web front ends, JavaScript
   libraries and ASP.net. I tested the different possible approaches in C# (WCF, ASP.net
   Web API + separate page, and ASP.net single page application with Web API) and finally
   decided to go for the single page application. I covered everything nicely with unit
   tests, created a solid data layout at the back end, and created a rather extensive AJAX
   front end using several JavaScript libraries. 

5. Review of round four: The project was uploaded to toptal’s git server. Afterwards we
   had the last Skype interview, where I explained my solution in detail, answered
   questions, and proved that the RESTful API works using Fiddler. Finally the interviewer
   welcomed me at toptal and instructed me about further administrative steps.

And this is how you get onto toptal.com as a developer. Currently I’m waiting for my
profile to be approved by an editor, which will also provide me with hints to improve it —
yes, they are that professional. If you happen to need a proven developer that also
completed this thorough interview process, head over to
[toptal.com](https://www.toptal.com/#pick-just-supreme-devs) (affiliated). They really
know what they are doing.

**Update 2018-03-28**: I still haven’t worked via Toptal, and probably won’t in the near
future, so I still can’t comment on anything after the interview process.  
When I wrote the article above, there was no affiliate program for toptal to my knowledge.
However, I added the affiliation to the toptal links above after I got aware of this
option. They are now also marked as affiliated.

**Update 2020-02-26**: I'm moving my website to GitHub pages and in the process I'm
tidying up the wording of this article and getting rid of the comment section. However,
I'm migrating useful old comments onto here as well (anonymized):

---

> E., June 9, 2014 at 20:22:  
> Thanks for sharing your experience here, very helpful. May I ask how long did it take
> Toptal team to approve your profile? Cheers
>
> > My reply, June 10, 2014 at 10:51:  
> > I’m still waiting… I contacted my last interview partner a few days ago, he said he
> > will look into it. Luckily I am currently occupied with some personal project.
> >
> > > My reply, June 14, 2014 at 09:43:  
> > > My profile is now approved:
> > > [https://www.toptal.com/profiles/15357/resume/internal](https://www.toptal.com/profiles/15357/resume/internal)

---

> i., April 25, 2017 at 09:31:  
> I would like to know about the question of round 3 and 4. What kind of questions are used
> to be asked. May be it will help me to prepare well for that level as well..
>
> > My reply, April 25, 2017 at 19:47:  
> > As stated in the article: String processing, a simple problem which involved choosing
> > the right data structure, and a simple web app.

---

> P., July 9, 2014 at 12:16:  
> Can you please tell the questions asked in round 3 (after codility test) ? it would be
> very helpful. Many thanks P.
>
> > My reply, July 10, 2014 at 15:25:  
> > I won’t give you the exact tasks, because that would take the hiring process ad
> > absurdum. They will also probably change with the individual interviewer. My first
> > task involved, as already stated, low level string processing. The second task
> > included the correct use of a hash map and file I/O.

---

> P., October 13, 2014 at 11:04:  
> What happens if you don’t do tests well? Do they let you take another chance later on?
>
> > My reply, October 13, 2014 at 12:37:  
> > Unfortunately I don’t know. Probably yes after some time, I don’t know for sure
> > though.
> >
> > > F., November 4, 2014 at 22:22:  
> > > Yup! After a couple months you’re allowed to try again.

---

> P., November 4, 2014 at 22:3:  
> Hey Benjamin, how has your experience been working with toptal??? Do they have a good
> amount of C# projects? Did you get the expected > hourly rate? Thanks for sharing your
> experience!
>
> > My reply, November 8, 2014 at 18:30:  
> > There are all kind of jobs on the platform. However, I found a long term contract on
> > another platform shortly after passing the Toptal interview. So I didn’t work through
> > them yet.

---

> S., August 12, 2015 at 09:23:  
> Hi. So, as I understand Toptal something like oDesk, but there they will offer you some
> contract, correct? I mean you can be a part of the TopTal’s developers, but you can work
> through them only when you want, correct?
>
> > My reply, August 12, 2015 at 12:17:  
> > It is like oDesk yes, but they only have hourly contracts. Also, Toptal is mainly
> > interacting with the client until you start working. When you apply for a project,
> > Toptal employees will have to approve that before the client sees it.

---

> B., November 15, 2014 at 19:59:  
> What about their terms in agreement:
>
> 1. 30,000$ penalty (always can say that you did it-and developer that not citizen of
>    toptal country can’t suite them in court in case they take money from his account):
>    if you “refer” ANY developers, engineers or technology related professionals directly
>    to Client,”you’ll be paying TopTal liquidated damages of $30,000
> 2. 2 first weeks can be unpaid in every project: If you’re not 100% satisfied after up
>    to two weeks of working with our developer(s),it’s free something totally wrong with
>    toptal terms – they just use that most people not read there agreement and sign it. I
>    think some people that work there should applied to US, Canada, EU, Russia etc
>    governments to avoid from toptal employee workers from there counties in such not
>    legal terms.
>
> > My reply, November 16, 2014 at 20:49:  
> > I totally see your point there. I’m not exactly at ease with what they write in their
> > TOS either (yes, I read it). However, in the end it might have just been written by an
> > overly careful lawyer. What is important, is how they *actually handle* these cases.
> > Do they use it do make a quick buck on one-time-offenders, or do they use it to punish
> > *real* leechers, that use Toptal’s resources to connect with top notch clients, and
> > then go on to promote their own developers. If the former was the case, we would read
> > it on blogs *everywhere*, and they would loose a lot of reputation. So I trust them to
> > handle these things as professional, as they handle everything else until now.

---

> M., January 9, 2015 at 10:52:  
> Hey Benjamin. I’m curious if it was worth all your efforts. Did you manage to land some
> good jobs and earn good money with TopTal?
>
> My reply, January 9, 2015 at 11:24:  
> > I only applied for jobs on Toptal for two weeks, since then I found a long term client
> > on another platform whom I’m working for since. Toptal seems to be slow in reacting to
> > applications, since every application is manually screened. Some jobs seemed
> > interesting, but I never was invited to any interview for the few jobs I applied for.
> > You have to take into account though, that there seems to be an emphasis on web
> > development, which is not my core strength. I think just being on there created some
> > kind of credibility for me, because I didn’t have any online experience or reviews
> > before.

---

> b., January 28, 2015 at 18:56:  
> Hi did any one made any money on toptal?
>
> > My reply, February 5, 2015 at 19:16:  
> > As I wrote above, I didn’t have a client via Toptal yet. I stopped applying after I
> > found my current one, and I wasn’t contacted for a job by Toptal either.
> >
> > > My reply, November 27, 2016 at 11:52  
> > > This is no longer true. I was since contacted several times by recruiters, usually
> > > with jobs fitting my profile quite well. I had to turn them down though, since I’m
> > > fully occupied.

---

> M., February 5, 2015 at 18:33:  
> Thanks for the review, Benjamin. I just saw toptal for the first time and they seem to
> be a notch better than the “standard” freelancer sites. I thought of giving it a try but
> wanted to look at other people’s reviews and comments first, as I have read quite a few
> negative comments about these platforms, especially freelancer.com. However, there is
> something odd about your blog post. You state on June 14, 2014 that your profile has
> just been approved by toptal,and you include the link. I looked at it and according to
> your profile, you have been a member since May 22, 2013 – almost a year earlier. So, the
> question is – how objective (and authentic) is this blog post? Or did you actually write
> it on behalf of toptal (which makes it advertising) in which case it really should
> include a disclosure to that effect? Sorry, but their T&Cs are quite one-sided and
> onerous, so I’d rather make sure first before signing up. Thanks.
>
> > My reply, February 5, 2015 at 19:30:  
> > Hey there M.!  
> > I signed up at the site during my research phase for becoming a digital
> > nomad to see what kind of projects are on there. Must have been May 2013, if you say so.
> > Unfortunately, without going through the interview process, one can not see the job
> > offerings. I therefore put the site aside and started the interview process when I
> > actually became a digital nomad in May 2014. Together with signups for odesk.com, tuning
> > my CV, creating this website and so on. I wrote this article about my actual
> > experiences. It’s the entry I would want to read before going through the interview
> > process myself. Unfortunately I can not tell you how easy it actually is to get a job on
> > there, how professional and quick the process is after the interview, or how strict they
> > apply their TOS. Nowadays I almost never check toptal.com, because I have found a stable
> > client via another platform. I will probably come back once my project is finished,
> > because I expect a higher hourly rate there, but it will by all means not be the only
> > platform I use. Toptal contacted me for writing a blog post for their engineering blog a
> > few months ago. Being a constant reader of this blog, I did write an article — I can use
> > the visibility. I now do get inquiries of prospective clients here and there, so at
> > least that worked for me. Good Luck with your search!
> >
> > > Z., March 18, 2015 at 17:04:  
> > > It now says “Member since November 22, 2013” – i think this blog post is an
> > > advertorial – it also show other jobs as part of his experience 🙂
> > >
> > > > My reply, March 21, 2015 at 10:14:  
> > > > I have no influence on what join date they display for me. And I basically wrote my
> > > > profile text on my own, but there was an editor from Toptal reading it and making
> > > > suggestions.
> > >
> > > M., February 6, 2015 at 09:30:  
> > > Hi Benjamin, thanks for the clarification – it’s a toptal feature, not a bug 🙂 My
> > > assignments can be anywhere in Europe and mostly involve working on-site with a
> > > client for months on end. This can be quite tedious at times, especially when the
> > > airlines periodically charge silly fares for commuter flights (great for airmiles,
> > > though). Like yourself, I am also considering a transition to a more remote work
> > > setup, i.e. digital nomad. Based on your experiences, I will give toptal and odesk a
> > > go, and maybe elance as well. Thanks for your helpful insights. By the way, I read
> > > your essay on VTK – excellent work! I have been using D3.js for some data viz work
> > > but VTK looks very promising,too. All the best!

---

> I., May 24, 2015 at 20:13:  
> Did you had in the end some time to experience a bit with Toptal? What’s your feedback
> now, after almost one year from being accepted?
>
> > My reply, May 25, 2015 at 21:40:  
> > I got a few offers with positions fitting my skills quit well, but I’m still working
> > with the same client full time, and this probably won’t change anytime soon. So no
> > experiences from myself. I met a young East European developer in Malaysia (also a
> > digital nomad) that worked full time via Toptal and he was quite happy with them.
> >
> > M., August 13, 2015 at 23:17:  
> > I wrote about the interview process a while ago and after being accepted, I am still
> > enjoying it. It is nice not to have to worry about billing, invoicing, and general
> > clerical work that I don’t have the time or desire to square away.

---

> k., May 21, 2016 at 21:00:  
> Hello Benjamin, Today I had a coding it was pretty tough..I failed. The test was in C
> programming and I could not complete it within time. What should I do to be better next
> time and after how much time do I apply for the same.

---

> S., September 2, 2016 at 11:31:  
> May I ask how much did you score overall in the second round?
>
> > My reply, November 27, 2016 at 11:59:  
> > I don’t remember the scoring system they use at Codility. I got maximum points on the
> > first two exercises, and 0 points on the third one, since there was no time for it.

---

> S., August 21, 2017 at 11:58:  
> So you mean, there’re 5 step in toptal test.
> Which step is the most difficult?
>
> > My reply, August 21, 2017 at 16:16:  
> > I’d say step 2 and 3, because it is coding under time constraints / supervision.

---

> N., September 20, 2017 at 17:33:  
> Hi Benjamin,
> Are there projects for C++ developer on TopTal?
>
> > My reply, September 21, 2017 at 18:43:  
> > There are some, yes. I also got invited to help with the Qt/C++ Desktop app Toptal
> > themselves are building (a time tracker). But most projects are obviously web-based
> > projects.

---

> S., September 25, 2017 at 20:06:  
> Hi Benjamin, In the 3rd step, I have to use camera for technical interview?
>
> > My reply, September 26, 2017 at 20:31:  
> > I don’t think it is required. I can’t remember.

---

> S., July 25, 2019 at 11:05:  
> Hi Benjamin, Are there projects for Oracle developer on Toptal?
>
> > My reply, July 25, 2019 at 12:12:  
> > I found two open jobs for the search term “oracle”, so it’s probably not a focus.
> > However, Toptal might be pre-filtering the jobs I can see, and “Oracle” is definitely
> > not in my skillset.

---

> A., January 18, 2020 at 23:08:  
> I have just started looking for a remote freelancing job. Seems you have been doing it
> for the past few years. Any tips you could share about some other options apart from
> Toptal? Web development is not really my fav thing to do as well. Have you managed to
> find another platform with good projects?
>
> > My reply, February 26, 2020 at 01:44:  
> > Yes, I've been doing it for a couple of years. Unfortunately I haven't found any other
> > platforms. All leads I got were from existing clients, or this website.

---

If you have any further questions regarding toptal, just shoot me an email to {% include
link_mailtome.html %} and I'll answer them by mail and add them here.
