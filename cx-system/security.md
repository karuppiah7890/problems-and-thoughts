# Security

## Assets

Some of the assets are mentioned below

### Code

Usually the system needs the code to run the tasks, like test, build etc. And
the only in the case of open source software, the source code is public, in all
other cases, it's private and very confidential and is the bread and butter for
many companies. It's a very essential asset!

### Secrets

Sometimes the system needs secrets to do tasks like - deployment to an external
system which requires authentication and authorization. 

## Vulnerabilities and Prevention

* Since the tasks have access to secrets, it's possible that they could log
the secret while logging the logs of the tasks. And the user viewing (accessing)
the logs may or may not have access to the secret, and hence it's not a good
practise to keep secrets open and lying around in logs. 

Another possibility is, the system could possibly log a secret that the system
itself does not know or hold, but that the secret is coming from some other
source, like the source code or some external system that the task is interacting
with.

A prevention strategy is to use a log processor, which will process the logs
before showing it to the user. While processing logs, whenever it finds the
known secrets in the log or when it finds a string of characters that "looks
like a secret", it can mask it with stars `*` or some other special character. 

The system could also warn the users or admins about this, so that it can be rectified.
