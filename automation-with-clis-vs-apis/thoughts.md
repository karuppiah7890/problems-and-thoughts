# Automation with CLIs vs APIs

By automation I mean automation scripts or programs
that do some automation to make our lives easier.
Automation with CLIs meaning - the automation
program code has CLI calls to do some work.
Versus APIs - REST/gRPC like APIs. This
comparison comes into place when the CLI is
not an offline tool, but a tool which connects
to some online service and does something.
So, let's take an example - GCP - Google Cloud
Platform. Now, to interface with GCP, there are
two ways that I know of - one is the gcloud command
line tool (CLI) and the other is the GCP HTTP/gRPC APIs
(I don't know what it supports, so 🤷‍♂). So, what's
the difference between using the two? I have noticed
that the gcloud CLI tool can be a bit slow, and it's
in python, so, whatever environment it runs in, it
should have the CLI tool along with python. Now,
many at times this is quite okay. It's all context
specific - right tool and solution for the right
job. My thoughts are this - if the automation is
like a one time thing or even if it run many times,
if the job done by the CLI is very less - then it's
okay - you don't have to take the trouble of
understanding the API of the online service and
writing some code to accomodate that to replace
the CLI, also you can also check the CLI code
which is usually open source to see how to
interface with the API and it's quite possible that
interfacing with the API is faster than running the
CLI tool, but it's too much work and code to do
if it's just a simple thing to do in the CLI tool.
So, when does one even opt for API calls?
Well, I have noticed some really bad cases
with CLIs where I think APIs can do better.
The case being - the CLI tool is called multiple 
times - like a gazillion times. Example is - a tool
our team built to get access to a GKE (Google Kubernetes Engine)
kubernetes cluster - for which we wrote the tool in
nodejs, and used gcloud and kubectl commands to
run and get access through an automation. This automation
runs on a CI pipeline of a repo which has multiple
YAML files containing information about who needs
what access - emails, along with cluster names,
and the level of access - similar editor, viewer etc.
Now, it was a really good solution. It worked very
well initially. I think this is what people call
GitOps. People put commits in the repo to get access.
But you see, every time someone put a commit, the input
to the automation increased - it had a lot of yamls
and data and had to give access declaratively -
give access if they don't have access, and remove
access if they have access but their data is not
in the repo. So, the git repo was the access management
thing for some custom access to clusters. It was kind
of inspired by declarative tools like terraform and
the declarative nature of kubectl. At some point,
we realized that the CI pipeline was taking a long
time to do it's work - giving access. This was
because, it was running gcloud commands one by one.
And kubectl too, one by one. Later a colleague
made it better by doing some batch operation
instead of individual operation when he noticed
that too many individual calls are being made
and the kubernetes server itself couldn't manage
so many requests. Nodejs can sometimes be too
fast, yeah. After that the CI pipeline was faster,
but still the gcloud commands were a bottleneck,
running one by one. I don't know if GCP API
has the ability to do batch operations, but if
it can and can do it faster than the one by
one execution of gcloud CLI, then I would
of course choose it! Agreed that it comes
with the cost of writing code for that
and maintaining it - compared to simple
CLI execution where CLI tool takes care
of things and CLI updates can be very easy,
but if speed is needed, we gotta do it.

So, I would recommend comparing speed of
the execution and the premise of the problem
too. Like, if it's an automation script
that's going to be run only once, or just
a very few times - like, very infrequently,
and if it's performance really doesn't bother
you, CLI solution is a really good and simple
solution :) But if it's going to be run a
lot and going to be used by many people and
at some point runs for a lot of time and is
not helping - and instead making people wait -
that can be really unproductive - similar
to slow running pipelines, slow builds etc,
so consider doing yourself a favor and check
the cost benefits of doing the same with an
API.

The same can be told for CLI vs library API.
And the library can be the CLI tool's API
code - and it can be for both online and
offline tools too. For example, `rg` is
a rust CLI tool, it's an alternative for
`grep` and it's really good at search.
Now, you want to use `rg`'s feature
in a program you are building,
what would you do? You can run `rg`
command using system calls to run
commands, more like exec calls.
But, what if you could directly
use the `rg`'s API, that is,
the library, the functions. Now, this
can be really useful if you want a 
lot of control over what `rg` does,
but if you just want a basic feature,
you can just do exec call and be done
with it. Like I said, it's based on
the problem, it's premises. You don't
want to over engineer and make a mess.
For example, since `rg` is written in
rust, now the question is about - do
you want to write your tool in rust?
It's gonna be a big yes if your tool
is like a wrapper for `rg` and you
want to do the best and even in that
case you can choose some other
language if you what you want to
provide is a wrapper, a library,
for another language, in which case
you just do exec calls. There are
costs to each solution and benefits
too. And benefits make sense only
based on the problem's premise.
So, think about different approaches
and weigh them and if you have time,
and want to really know some numbers,
may be even try them and weigh them :)

In the above example, we used nodejs
to call the CLI tools `kubectl` and
`gcloud`. `kubectl` is written in
golang and `gcloud` in python.
But they are only CLI tools for a
running service, which has an API like
HTTP/gRPC API, which are language agnostic,
so you don't need to use the golang or python
library functions, you can instead interface at
a different level in the same language that
you are working in :)
