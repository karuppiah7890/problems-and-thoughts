# Backward Compatibilty

I think many might know what backward compatibility means. I learned it from
people and from some random text I guess. I just found out some formal links to
it -

https://en.wikipedia.org/wiki/Backward_compatibility
https://en.wikipedia.org/wiki/Backward_compatibility#Software

I usually like to think of the meaning of backwards compatible like this -

There's a system `S1`, which has been built and it takes input and gives output,
where input and output can be anything. Now, let's say you build another version
of the system `S2` with the same source code, or you build a totally new system
from scratch or something like that, but the systems are related and are trying
to do the same thing or may be the new one is trying to do more things. Now
the new system `S2` is called as backwards compatible based on the below
conditions

![backward-compatibility](images/backward-compatibility.svg "Backward Compatibility")

I'm going to tell this in a more mathematical way:

If `Input 1` is the input to `S1` and `Output 1` is the output of `S1`,
and `Input 2` is the input to `S2` and `Output 2` is the output of `S2`,
then **If** `Input 1` is equal to `Input 2`, and `Output 1` is equal to
`Output 2`, then the new system `S2` is said to be backwards compatible with
the old system `S1`. 

BUT, **If** `Input 1` is equal to `Input 2` and `Output 1` is NOT equal to
`Output 2`, then the system `S2` is said to be backwards incompatible or
having breaking changes, because of which the user has to change their input
to the new system `S2` to say `Input 1'` to get the desired output `Output 1`
that they got with `S1`

In more simpler terms, given the same input to old and new systems, if the
output is the same, the the new system is said to be compatible with the old
system. If for any reason, for any input, if that does not hold good, then
the new system is said to be incompatible.

How does one know if there's been a breaking or incompatible change in a
software system? Does everyone have to check the source code, run some
functional tests and check if the new system is compatible? Well, there are
ways to do that.

## Semver

People usually version their systems. For example `v1`, `v2`, `v3.4` etc.
They usually use some versioning method. A famous one is https://semver.org/ ,
Semantic Versioning. It has details talking about how the version number
should be changed to show if the new version has changes that are breaking/
incompatible changes, or just has new changes, or has fixes to bugs and that's
it. 

Even if semver is present, it doesn't mean people properly follow them. It
would be great if every team follows it holistically. It's especially useful
when tons of people are using the software, a software that's too big with a
big community and people are running the software in production etc. Any
serious software will try to follow some versioning and stick to it. 

## Changelog

Even with semver and stuff, another thing to checkout for understanding new
versions or new systems is - changelog. Usually softwares release their
softwares along with version number AND changelog too, mentioning the new
changes that have been made, at a high level, in a log or list like format - log
of changes, something like that. The changelog usually mentions if any
breaking changes have been made and what new features have been added and what
fixes have been done. So, it's a good place to look at if you are looking to
find backwards incompatible changes.

## Libraries

What does backwawrds compatibility mean for different softwares? In terms of
libraries, usually they provide APIs - that is functions, methods, types, and
what not, for some feature / functionality. And developers use some package
manager of sorts to manage their packages / libraries / modules / dependencies
(too many words for the same thing 🙈) and get the libraries from some place,
usually called a registry of packages. Now, when new versions of libraries
are released, and developers upgrade their libraries to the newer version,
if the developers don't have to change a single line of code related to the
library during this upgrade - it means that the new version if backwards
compatible. If the new version is a breaking change, the source code would not
work as expected and developers would have to change the input to the library -
for example, change parameters, types, invoke the function with a different
name as name has been changed etc. That's how it would look like for libraries.

## Mobile Apps and Services

Let's say you are building mobile apps and you have backend services for these
mobile apps. Remember, you have two separate systems now - mobile apps and
backend services, usually each has it's own versioning based on the changes made
in each.

Mobile apps access the backend APIs to work correctly. So, let's say you have
mobile app version v1 and backend service v1, and everything works well. Now,
one fine day you make changes in one of the existing endpoints in the backend
service and release it, with no changes in URI path, request method etc, but
only a change in the API response - you rename a field. And if the mobile app
version has not changed, and uses this endpoint, it will break because of this
rename - this is because the mobile app would have been written based on a
contract of the API, expecting the API response in a particular schema /
structure. Now this is inevitable and may be something you already know, if
you are working with backend services or front end systems like web app or
mobile app or desktop app, interacting with backend APIs. So, how does one
tackle this kind of problem?

First of all, surely there must be some testing mechanisms, to make sure that
the mobile app and the backend service work together - there must be integration
tests to help with this. Every time the backend service is released or the
mobile app is released, an integration test suite must run to check if they
work together.

When making changes to the backend service, one must understand what's a
breaking change and what's feature addition, or a bug fix. Usually bug fixes
can be done with 0 changes to the API request or response schema / values.
And API contract is the main thing in our case. It's like the API of libraries.
You need to be careful when you touch the API, the interface. For feature addition -
adding features without changes in API contract is awesome - I guess the only
change will be in the API description, or one might add new endpoints to the
API, or features like - adding new query params to GET endpoints, for example
query params for pagination in GET request. These are just some examples.
Another example is adding an extra field in an API response. That's not a
breaking change usually - as the client using the API usually just reads the
response and uses only the parts of the response that it understands, so, if it
doesn't know about a field in the response, it doesn't care, usually. But if
you have some strict contracts, such that if any field is extra in the API
response, then the client will throw errors, that's something you need to take
care based on how it will affect you. So, what are we talking about over here?
When we talk about new fields or similar changes in backend service that is.
Also, remember, you are making changes in backend for the mobile app's newer
version in this case.

Let me show some diagram to you, for the situation I'm talking about -

Mobile App v1 and Backend Service V1
![mobile-app-and-backend-service](images/mobile-app-and-backend-service.svg "Mobile App and Backend Service")

In the above case, your mobile app and backend service are compatible and the
version is v1 for both.

In this case it looks like both app and service have same version numbers, but
it's just for simplicity we have put this. It's very possible to have totally
different version numbers, for example v1.25 Backend Service and v1.35 Mobile
App, or something totally different too, like different major versions, and
still be compatible

Also, Mobile Apps can have breaking changes too - for various reasons and they
will be called breaking changes due to different reasons and parameters, for
example, based on my imagination, since idk too much about how mobile apps
are versioned, let's just say - removing an import UI component that was
previously present could be considered as a breaking change. But it may
still work with the Backend Service that's running.

But yes, at some point you might have breaking changes in the API, and
new changes / features are going to be there always in both the mobile app and
backend service. And if new features in the mobile app need new features in
backend service, then new version of backend service with the new features must
be present for the new version of mobile app to work. So, even for deployment,
you deploy the backend service first and then release the mobile app. The thing
is - at some point, you will have to put a matrix - to tell what version or
versions of mobile apps work with what versions of backends. The reason for
mobile app not working could be because - some feature is missing in the backend
or because there's a breaking change in the backend. And you will also be
writing code in the mobile app to change the way it interacts with the API as
the API would have changed now, due to new features or breaking changes, and
this mobile app now has a different version too. I'm going to talk about how
to accomodate these breaking changes or new features.

For new features in API and mobile app, without breaking changes - for example,
there's an extra field - extra data, which you want to show the user in the
UI. This extra field comes in the existing API endpoint. The old version of the
app uses this same endpoint, but there's no code in it to consume this new
field and it's fine, as there's also no code in it for the UI to show this
new data. But in new version, there's code for consuming the new field in the
API and to also show it in the UI to the user. Now, this feature does not harm
the old versions and gets new features to the people who are using the new
version. And there's only one version of the backend that's running. See
image below

Now, we have new version v1.1 for both Mobile App and Backend Service. 

![mobile-app-and-backend-service-different-versions](mobile-app-and-backend-service-different-versions.svg "Mobile App and Backend Service Different Versions")

Now, let me give you very specific example so that it's more clear to you, which
is important for the next concept I'm going to talk about.

We are building a social media app, and we have an endpoint for creating
a comment in a post, for example 

```
POST /v1/posts/{postID}/comment

Content-Type: application/json

{
    "text": "this is awesome! thanks for sharing!"
}
```

```
GET /v1/posts/{postID}/comment/{commentID}

Content-Type: application/json

{
    "text": "this is awesome! thanks for sharing!"
}
```

Now, in a new version, we want to introduce tagging feature, so that users can
tag each other in comments. For this, we decided to change the endpoint like
this

```
POST /v1/posts/{postID}/comment

Content-Type: application/json

{
    "commentsWithTags": [
        {
            "type": "MENTION",
            "userData": {
                "userID": 567,
                "username": "@karuppiah7890"
            }
        },
        {
            "type": "TEXT",
            "text": "this is awesome! thanks for sharing!"
        }
    ]
}
```

```
GET /v1/posts/{postID}/comment/{commentID}

Content-Type: application/json

{
    "commentsWithTags": [
        {
            "type": "MENTION",
            "userData": {
                "userID": 567,
                "username": "@karuppiah7890"
            }
        },
        {
            "type": "TEXT",
            "text": "this is awesome! thanks for sharing!"
        }
    ]
}
```

But as you can notice, this would be a breaking change. The same endpoint is
being used by the old version of the app and the new version of the app will
use the same endpoint too, but both are expecting different output. Now, that's
not possible. The old one is going to break for sure if you bring this feature
like this. Now, what are the different ways to solve this problem?

1. You can force all your users to upgrade to the new version

Now, this is a big call, as you are forcing all your users to upgrade and not
all may not be able to do it - due to different reasons - for example, due to
no space in phone and your new app being bigger, or not much network / Internet
to download the latest version etc. And it can also be annoying to force the
user. But yes, it's possible - you can write some UI code and stop the user
from using the app and ask them to update the app - you can use the API's
response to check what version of the mobile app is supported by the API that
the app is accessing.

2. Change the api version in the URL

Instead of reusing the `v1` in the URL, you can change it to `v2` like this

```
POST /v2/posts/{postID}/comment

Content-Type: application/json

{
    "commentsWithTags": [
        {
            "type": "MENTION",
            "userData": {
                "userID": 567,
                "username": "@karuppiah7890"
            }
        },
        {
            "type": "TEXT",
            "text": "this is awesome! thanks for sharing!"
        }
    ]
}
```

```
GET /v2/posts/{postID}/comment/{commentID}

Content-Type: application/json

{
    "commentsWithTags": [
        {
            "type": "MENTION",
            "userData": {
                "userID": 567,
                "username": "@karuppiah7890"
            }
        },
        {
            "type": "TEXT",
            "text": "this is awesome! thanks for sharing!"
        }
    ]
}
```

What does it mean to choose this solution? If you choose this solution, remember,
your old version of the app, still uses `v1` comment endpoint. So, now you need your
backend to support both these endpoints somehow - either by running two different
versions of the app in different instances and do some routing using web servers
(like nginx etc) or in the latest version of the app, support both `v1` and `v2`
comment endpoint. And remember, whatever approach you take, the stance is - you
need to support `v1` comment endpoint, which means make sure `v1` comment
endpoint is accessible and working and also, if there are any bugs / issues, you
will have to fix it. Of course you will not bring in new features or fields to `v1`
comment endpoint as you cannot change the code of the old mobile apps and only
they use the `v1` comment endpoint and here after the new versions will be using
`v2` comment endpoint. Mind you, there are still other endpoints under `v1`,
for creating posts and what not. Only comment endpoint is present under `v2`.

It will look like this

![mobile-app-and-backend-service-different-versions-v1-v2](mobile-app-and-backend-service-different-versions-v1-v2.svg "Mobile App and Backend Service Different Versions v1 v2")

Also, for this whole thing to work, now you gotta make sure that there are no
disruptions to the users, so, when a user from old mobile app comments, the
backend should store in the database as a simple text, and when they request
for data, it should come as simple text data, even if the comment was done
by a new app user and they sent the data in a complex JSON format. So, the
backend has to handle the data and make sure that it sends response accordingly
to the different kinds of users, a matrix is below, and all should work

    * New App user comments, Old app user views the comment
    * Old App user comments, New app user views the comment
    * New App user comments, New app user views the comment
    * Old App user comments, Old app user views the comment

Now, this can get cumbersome, you know, supporting two endpoints, and the code
for both will just live. More maintenance. But yeah, it's one possible solution.
Actually, I have seen this kind of solution being used when the API developers
don't know who is using their endpoints and if they have no control over their
clients - which is very possible in the case of a microservices architecture
and when the clients are microservices and all of them are being built by
different teams. In our case, the consumers are mobile apps alone and we do
have control over the clients through some way, let' say. ;)

3. Add an extra field to the API response

You can try this. For old app, it will keep using this `POST` endpoint

```
POST /v1/posts/{postID}/comment

Content-Type: application/json

{
    "text": "@karuppiah7890 this is awesome! thanks for sharing!"
}
```

and when using `GET` endpoint it would get this kind of data if it was the
one that created the comment

```
GET /v1/posts/{postID}/comment/{commentID}

Content-Type: application/json

{
    "text": "@karuppiah7890 this is awesome! thanks for sharing!"
}
```

And for the new app, for the same comment it would look like this -

```
POST /v1/posts/{postID}/comment

Content-Type: application/json

{
    "text": "@karuppiah7890 this is awesome! thanks for sharing!",
    "commentsWithTags": [
        {
            "type": "MENTION",
            "userData": {
                "userID": 567,
                "username": "@karuppiah7890"
            }
        },
        {
            "type": "TEXT",
            "text": "this is awesome! thanks for sharing!"
        }
    ]
}
```

and when using `GET` endpoint it would get this kind of data if it was the
one to create the comment

```
GET /v1/posts/{postID}/comment/{commentID}

Content-Type: application/json

{
    "text": "@karuppiah7890 this is awesome! thanks for sharing!",
    "commentsWithTags": [
        {
            "type": "MENTION",
            "userData": {
                "userID": 567,
                "username": "@karuppiah7890"
            }
        },
        {
            "type": "TEXT",
            "text": "this is awesome! thanks for sharing!"
        }
    ]
}
```

And if old app comments and new app gets the comment, it will first check
if the `commentsWithTags` field is present, if it's not, it will use the `text`
field. The old app always uses the `text` field as always and the new app makes
sure to give the backend the `text` field too. The only small thing to note is -
there are two forms of the same data, one is simple text form, another is a
complex list of objects. The one thing that can go wrong with this design is,
one can put different data in the two fields, so the mobile app should work
correctly and put the correct data, or the backend has to be intelligent and
do some checks.

Now, this way, the new app can actually show the comments in a beautiful way,
by using the extra data if it's present in the API response, which means a
new app user commented that comment, and it will bold the mentions of users
with the data it has and also navigate to the user profile when the user mention
is clicked. The old app will always show simple text, as it's old code and does
not have this feature.

If you can note, this kind of problem comes up when you cannot exactly control
the clients, which is possible when it comes to mobile apps, wearable apps,
command line apps. You can ask them to upgrade, force them too, and may be auto
upgrade if that's possible. But still, it's a thing. You need to make them
upgrade or upgrade it somehow with your code, which should already be present
in the app that you have shipped. This is not the case in web apps though, where
you can ship the new HTML, CSS, JavaScript, and even if you have offline support,
Progressive Web Apps (PWAs) with front end cached, I believe there are ways to
invalidate the cache to serve new versions of the code when needed. That way,
it's easy to upgrade the client code when the backend code changes, API changes
and you probably don't have to support older client code and always be on the
latest code in the client side.
