# Interaction

`How the user interacts with the system?` is a key question that needs to be
answered.

The answer needs to consider a lot of things, for example the use cases that
the user has, and the different kinds of users.

Let's assume the system has some form of access control, for example, RBAC -
Role Based Access Control, where there are different roles. It's a famous
access control mechanism.

Let's assume we have users with different roles and then admins. We can think
about the possibility of static / dynamic roles. Dynamic roles meaning - 
users can define a custom role with a very specific set of permissions.

Now, with the current era, there are many ways a user can interact with the
system. GUI ways - web, desktop app, mobile app, wearable app, tv app, CLI ways -
command line app. And for automation, the user will need access to APIs too.

Since this is a CI/CD system, based on the audience, supporting tv apps,
wearable apps, mobile apps may not be really required, unless the users are
asking for it. Research can be done on the same.

To start with, support web, the ubiquitous platform, is a good call, and
supporting command line tool and APIs too, for automation.

`How does the user give input?` is also a key question to be answered.

Many systems have followed to get the input by keeping the input as part of the
source code in the form of a config file. A config file which configures the
tasks to be run and all the information that the CI/CD system needs to run the
tasks

Many systems have used `YAML` format/language for their configuration file.
And they define their own DSL (Domain Specific Language), which the user has
to use to give input to the system in such a way that the system can understand.
The systems also provide linters to validate the DSL.

Other possibilities:
1. Config file with other formats like `JSON`, `TOML` etc
2. Write code in a programming language or languages, based on what the system
supports. The system can provide a library - a development kit, to access it's
APIs or features, and the user can write code to tell the system which / what
tasks to run and how and what not. Pros - lots of freedom. Cons - Not sure, may
be lots of freedom is a con too, given that anything is possible with so much
freedom - it could become a complex system? May be.
3. GUI method to provide input. Pros - very less learning curve. Cons -
automation could be hard, if the config files need to be created in an automated
manner. To avoid the cons, the GUI can export the input in a particular file,
that the system supports. And point 1, can still hold good, and help with
automation.
