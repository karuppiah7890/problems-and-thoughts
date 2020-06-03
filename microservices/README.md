# Microservices Architecture needs and Organizational stuff

The below information is based on my experience with microservice architecture
in a company.

Microservice Registry:

When there is an organisation with too many microservices and it keeps scaling,
you will need some form of registry to know information about these microservices

This can be information like
1. The name of the microservice
2. Description of the microservice
3. The team owning the microservice
4. Tech lead's email or team's group email
5. The codebase link
6. Information about the different environments it has been deployed to.

    For example in a project I was in, to support multiple countries for the
    products, but not all products in the company, the decision was to separate
    infrastructure for each country and deploy only some microservices there,
    based on the products supported in the country. This meant that, there
    are many environments - based on the country, and then based on the kind
    of environment like - Dev/development, Testing/QA, Staging/Integration,
    UAT/User Acceptance Testing, Prod/Production. In that project, ideally a
    microservice will be deployed uniformly to all kinds of environments, but
    when it came to country, it would be deployed to a country's infrastructure
    only if the corresponding product or feature is open in the country. So,
    we needed information like which microservices are deployed in which
    country environments including the kind of environment.

7. The different processes in the microservice.

    Like servers and workers. That is, for each process, include
    - Process name
    - Process type
    - Command to run the application
    - Command to run the migration if one is present, in case of a database
    - Number of replicas for the process

All this information needs to be periodically checked and updated with the right
information or the data goes stale. It needs lot of human input and interaction.
The system could nudge the teams to check and update information every X days.
This is similar to how online services nudge users to update their recovery
email ID and phone number and confirm if it's still good and updated. And also
nudging or forcing users to update passwords for safety reasons.

This registry information will help in
1. Finding which team a microservice belongs to. It's hard in organizations with
too many teams and microservices. And it's useful especially when you want to
know whom to contact to get help with respect to a microservice, for some
production issue or for any thing, like just to do development and another
microservice is related / involved.
2. When you want to make sure that all microservices have an owner, that is, a
team. Sometimes some microservice are orphaned, and many teams take care of it
based on need. This usually happens because the microservice is usually mostly
stable or is being rewritten or something. And also, many teams might be helping
because the microservice is helping multiple teams and probably the features are
used across many microservice. So, it's like, it's everyone's problem, but no
one picks it up or owns it sometimes, thinking they already have too much on
their plate with respect to core team's work and it's own microservices and then
think someone will pick it up, that is, wait for someone, and when everyone
waits, it's like no one's problem. So, people usually say that such cross
cutting things, which affects multiple teams and has no owner, is like
everyone's but no one's problem. But it's important to have one owner (one team)
at least, for every microservice. This is to provide support and to maintain the
microservice.
3. Understand the scale at which the company is operating. It's scary when you
don't even know how many total microservices you have, and what each is doing.
4. Automated deployments. Since you have a lot of information. If you have the
right access, you can access this system to get information and deploy a
microservice with a single command may be
6. Feeding information that infrastructure teams need. Infrastructure teams keep
doing different stuff. Like trying to evolve the architecture, the infrastructure,
which usually means migrating from the old one to a new one and it needs a lot
of information, and also automated deployments and also a means / way to connect
to the right teams to discuss about the migration to get help etc. This kind of
system helps a lot in such cases!

---

Automated and seamless Deployments:
Devs really don't need to manage infrastructure or even worry about it. They
usually have just enough time to develop the feature in a scalable manner and
want to deploy it and be confident that it will run and work, always. To help
with this, many systems have been developed in the last few years in the devops
space. PaaS - Platform as a Service, is a general system, that provides users
a place to just put their code and the platform takes care of building and
running it based on some scripts and based on the code, and then gets input
regarding resources (CPU/Memory), number of instances, configuration and that's
it. Some automated and abstracted deployments I have seen are:
1. Abstracted deployment to Kubernetes
2. Abstracted deployment to VMs

Automated deployments: Level of control for a dev? I think the following
can be controlled by devs
1. Code - particular version of the code. Best thing is Commit Sha
2. Replicas
3. Resources - CPU, Memory (RAM)
4. Configuration - Environment variables (ideally) or configuration files
5. Where to deploy?
6. Exposing the service externally to the Internet
7. Exposing the service internally to the VPN
8. Kind of deployment? Rolling update, canary
9. Migration command to run
10. Init command to run

Devs need not really worry about where their service runs - VMs or containers,
in some cluster or something. They also shouldn't need to worry about how to
run it with high availability, and making sure that it's running with 0
downtime in terms of infrastructure

---

Configurations and Secrets:

There's more to a process. For example, what about the configuration and secrets
required for a process / microservice? Usually people consider non secrets as
configuration, and secrets as secrets. I think that configuration is also a
general word.

Now, you can either consider non-secrets and secrets separately and manage them
separately, or consider them the same, like, consider all of them as secrets and
manage all of them as secrets, less complexity in management and also,
everything is secure by default! You can use cloud provided services to store
your secrets. Or host a something on your own and use it, something like vault
and then see how to use in your deployment for the service. Usually if you are
following 12 factor app methods, you will have every configuration as environment
variables. And also, do consider the possibility of requiring configurations to
be versioned, the pro to that is - you can easily revert back to old
configurations if you have all the versions. Think git, but for configuration!
For example, Vault has versioning. Also consider audit changes to configuration,
like when configuration change was done and who did it, this is just for safety
purposes. Again, for example - Vault also provides audit logs. 

---

Team and member management

A management system to tell who belongs to which team? It's hard to tell in an
organisation which is quite big

This will system will help in
1. Alerting another automated access management system through an event with
details, when someone is added to the team or removed from the team, which in
turn will help in providing and revoking access in an automated manner

---

Automated access management:
1. When someone's added to a team, based on the team, they will require access
to different kinds of things, like:
* Source code
* Project board like Jira, Favro
* Infrastructure - The cloud, VMs, Kubernetes cluster, logs etc
* Other services like
    * APM (application performance management) services like New Relic, Data Dog
    * Documentation services like Gitbook, Confluence etc
    * Alerting services like Pager Duty
2. Revoke all access when someone is removed from a team

---

Alert system metadata and alerting system
1. This should have metadata at least, to store all the data related to
alerts - for every team, what are the different channels for alerting - pager
duty, slack etc and the information regarding these channels. This will help
to route any alerts to the right channels based on the team the alert has to go
to. This is really helpful to route the alert to the right team, because if a
service belonging to a team raises an alert, then that team needs to be alerted
correctly.


The above talks about the input needed to route alerts to team, for which first
alerts should be raised. In general, there needs to be a system to raise alerts
based on some sort of metrics, for which metrics needs to be collected first.
For everything going on in the system, useful metrics needs to be collected.
This is all part of monitoring the system. Examples of systems that can help
with metric collection are Prometheus, Influx DB. Prometheus can also do
alerting, and works well with alert manager, an tool in the same ecosystem, that
can help with managing alerts, like where it goes to, and also, grouping alerts,
silencing alerts. 

---

Debugging microservices
* Open Telemetry?
* Distributed Tracing?
