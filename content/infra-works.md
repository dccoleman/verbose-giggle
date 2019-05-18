---
path: "/blog/may-19/infra-works"
date: "2019-05-18"
title: "Infrastructure is working"
---

# Infrastructure

Infra is as follows:

On a push to master, github webhooks call an api gateway endpoint. The lambda at the other end checks if it's a push to master, and sends an SNS notification if so. There's an SQS queue listening on that SNS topic, which triggers a lambda to request a spot instance. That instance installs node, npm, git, and gatsby, and runs the build and deploy scripts in the package.json. SIMPLE.

## current bugs

I'm not correctly filtering the github webhook events, so two spot instances get spun up instead of one..
