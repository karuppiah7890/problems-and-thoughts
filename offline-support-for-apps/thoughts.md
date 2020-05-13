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
