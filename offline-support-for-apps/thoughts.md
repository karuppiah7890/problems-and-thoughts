# Offline Support for Apps

This depends on the app - web app, desktop app,
mobile app. The common thing is, they are online
apps, that's why the "offline support" term comes
into existence. It doesn't make sense to think
about this if the app works completely offline -
without connecting to the Internet, even if the
Internet is enabled.

So, now, let's say the app gets data from the
Internet to show it to the user or for it's
working, there should be some way for it
to work offline if it's possible. Usually
it's possibly unless it's some app that
completely depends on the Internet and
on a central server - for example an
online multiplayer game with no
single player? Something like that.

Now, let's take an example of a social
media app. I'm part of a team that
builds a social media mobile app. We
were talking about offline support.
More like, how do things work if
the user is offline - that's what
offline support is all about, right?
For example, I open up my mobile app,
see some posts, and then lose network
signal in my phone, so I have zero
Internet now. I close the App. I open
it again, what happens now? Do I still
see posts? Or a blank timeline?
Clearly a blank timeline is bad.
Let's say I can see whatever posts
I scrolled through in my timeline,
but, now what? I'm offline, so, I can't
like/share/comment? If it's possible,
it's better if we do it. Right?
Even if you say that you cannot
support multiple features when
my Internet is off, that's okay, but,
what about the case of a bad bandwidth?
Many places in the world still have a
bad Internet. Also, many people in the
world cannot afford good Internet even if
it's present in the place they live in.
Internet prices differ from place to
place. So, if you want to support a
lot of people to use the app, check your
audience and check how to support offline
usage. Also, even if people have good
Internet, it doesn't mean you can use
it as much as possible and hog it. A
lot of apps might need Internet, so as
app developers, we need to diligent about
how we use it.

Some ideas I think people are implementing
for offline support is - use local caches.
I think that's like a baseline thing now
a days? So, in the case of mobile apps,
use a local cache / local DB, where you
store things. In the case of our app,
it's an Android App, social media App.
We use SQLite. So, we store the posts
in SQLite. Some things that can be done
for offline support are - allow
users to comment, like and share posts
even if they are offline. Store all these
actions in the SQLite DB. Later, sync these
actions with central server when the user is
online. This is a really good experience.
Also, even if user is online, I think
some optimizations for action updates can
be done - that is - for any user
action - first store it in
local DB and then sync DB info with central
server every few time intervals t, like 30
seconds, 1 minute. One Pro is - you can try
doing batch updates in your API calls may be?
And also may be in an efficient manner?
Which is better (smaller in size together)
than doing API call for every action - like,
comment etc. I don't know if it's possible,
but if it is, I would go for it!

Next thing is how long to store the cache
in local DB? We chose to retain data for
30 days. I have to check how we do that.
I just joined the team. Before asking, I
was thinking myself, what kind of data
retention would make sense? Let's say
30 days is a good number - meaning
I will have the data of the past
30 days. Now what? Well, this
depends on the application and what
the product wants to support. For
example, in our use case, for a social
media app, let's say I'm very active
usually. And then later, I use
Digital Wellbeing app and put
a 0 minutes timer on the app, so
that I don't use the app for one
month. Or let's say my Internet is
broken or my phone's broken or
something and for some reason,
I was not online for one month,
or at the root level - my social
media app could not connect to it's
servers for one month, due to some
reason. But app is present - installed
and cache is there. Now, after a month,
which is roughly 30 days, I'm still offline
and I simply open the app - should I see posts?
or not? This is a call you can take. Now, if you
ask me, I would say - why not? I mean, I can't
go online, but whatever is in my cache - let it
just be there may be? Let the user have fun
checking out the posts or whatever? But if we
want to do that, our retention time of 30 days
doesn't work out then. As it's already 30 days.
Then, should we extend that? Will we keep
extending? I was thinking about - how about
we get the last active time of the user -
the last time the user was online - with
this information - what we can do is -
we can say - have past 30 days worth of
cache since the last online active time
for the user. This way, if the user was
active in app about two months ago, and
then was never online, even though they
had the app, the data in their app will
be there - it will be data of -
(last active time - 30 days) to last active time.
This also means that the app is using up that
much of the user's phone storage. That's
also something to note and take a call
on. May be consider not storing much
like 30 days that we have, if the user
hardly checks the app when offline, at
some point, we can ask the user if they
want to clear the cache or we can do it
automatically if we feel we should not
hog the user's phone storage. Each thing
has it's pros and cons. So those were my
thoughts on it. Also, it very much depends
on the app - for example YouTube, Netflix
may not want their users to be able to
download content for offline viewing
and view offline for a long time.
Especially given Netflix is a paid service -
as this can also mean that - the user
can con / game the system. Let me explain how.
I'll explain as a timeline

T1: user gets access to Netflix, through some
way (trial, paid for subscription, etc)

T2: user gets Netflix mobile app, downloads
some videos for offline watching. and goes
offline

T3: user still hasn't come online in Netflix.
Netflix stops the user's service due to some
reason (deactivation, trial ends, fraud etc)

T4: since user still hasn't come online,
and the Netflix mobile app is still present
in their mobile and the downloaded videos are still
present for offline viewing.

Now, the above is a problem. So, for this reason,
after some retention period, Netflix invalidates
the downloaded videos that you have for offline
viewing and asks you to "renew it" - for which
you need to come online - that way Netflix can
validate your subscription and then mark the
offline downloaded video as valid for viewing
offline as you still have access.
I think something similar is present for YouTube.

And in case of Netflix, it will also validate
if the video you downloaded is valid to
watch in the country you are present in.
For example, if you go to some other
country, say USA, which has content that you cannot
watch in your country, let's say India, which is
the case for me, and then you download the
content when you are present in USA and then
when you come back to India, after the said
retention time, it will mark the content as
invalid and then ask you to renew and while
renewing, it will also make sure you can still
watch the content in the country you are
currently present in. In my case, if I come
to India after downloading USA only content,
it will get invalidated later saying I can't
view it in India. :/ Netflix is too clever :P
Of course. :P
