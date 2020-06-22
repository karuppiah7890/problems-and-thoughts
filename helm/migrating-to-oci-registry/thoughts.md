# Migrating to OCI registry

Recently, in the Kubernetes Slack `helm-dev` channel, there were some
conversations around Helm Chart Repository and the OCI (Open Containers
Initiative) registry and about migrations if needed

Check the conversation using these links

Question link
https://kubernetes.slack.com/archives/C51E88VDG/p1592496833461200

There were some answers to the question, but it wasn't a thread, but finally
a thread was started over here

https://kubernetes.slack.com/archives/C51E88VDG/p1592497850465500

Screenshots of the conversation are below

![1](images/1.png "1")

![2](images/2.png "2")
![3](images/3.png "3")

I was thinking if I should create a tool to help people download all their
charts in the chart repo and migrate it to a OCI registry ;) Let's see :)

---

The input to this tool would be - which repo to migrate and to which OCI
registry.

For example, it could be like

```bash
$ helm oci-migrator migrate <repo-name|repo-url> <oci-url>
$ # example
$ helm oci-migrator migrate stable localhost:5000
```

This will push each chart as an image which will look like
`localhost:5000/<chart-name>:<chart-version>`

References:
https://karuppiah7890.github.io/blog/posts/helm-3-charts-and-oci-registries/
