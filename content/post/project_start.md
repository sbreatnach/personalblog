---
title: "Starting a New Project"
date: 2022-06-04T06:14:28+01:00
draft: true
tags:
  - Microservices
  - Service-Oriented Architecture
  - Software Engineering
categories:
  - Technical
---

When starting a new software service that will be used by a wide audience, there's a lot of things to consider. Otherwise you could hamstring the project further down the line. What I'll do here is present the full list of things to keep in mind. Exactly how you implement this is entirely up to the technologies you use. This list is with a web service in mind but a lot of it is applicable to any software project. In the end, I think these are all concepts and solutions universal to modern software engineering.

<!--more-->

## Web Handling

* Use RESTful APIs for all but the most specialised APIs. They are the most portable, easiest to document and are universally usable (even by microcontrollers!).
* Support HEAD, PATCH, PUT and DELETE verbs, even in obscure proxy environments.
* Try to follow RESTful principles.
* Use HTTP status codes correctly - they are the closest to a universal error code system you will find.
* Version every API, internal and external.
* Every API should log who and where connections are coming from. This is invaluable when you're trying to find out who's consuming the API.
* Internal API consumers should send extra HTTP headers to identify themselves.

## External Integrations

* Every outgoing connection from a service must have a timeout.
* Every outgoing connection must have a retry mechanism.
* Every retry has an upper limit of attempts by default to work around blips in the external service.
* A retry may be configured as never-ending - useful for batch processing or recovering DB connectivity
* Every retry must have an exponential back-off timer.
* Every retry can be cancelled.
* Every retry should have configurable jitter.
* Every active retry should be modifiable to help out in disaster recovery situations.

## Configuration

* Have a configuration system - any variable that could be modifiable in the future should be.
* Support basic data structures and primitive types at a minimum (e.g. lists, integers, booleans, etc.).
* Allow for reloading configuration while service is running (SIGHUP is the convention in Linux).

## Logging

* Support multiple levels of logging - clearly define what type of logs should go to which level.
* Log levels must be configurable.
* Use structured logging (but not at the cost of difficult to read logs).
* Sanitise logs to remove sensitive information (e.g. emails, passwords.
* Have trace level logging to support debugging live systems.
* Trace log health pings to reduce noise.
* Gather system logs external to your service.
* Use a logging backend that collates logs from all parts of the system.
* The logging backend should take advantage of structured logs.
* Retain one month of trace log data, at a minimum three months of logs for all other levels.

## Monitoring

* Always have a health endpoint
* The health endpoint should fail if any required infrastructure is inaccessible.
* Always include a metrics collection system
* Decide on a naming convention for metrics data points that is documented
* Use a metrics gathering system external to your main project.
* Have a sepate metrics gathering system for the main metrics gathering system (quis custodiet ipsos custodes?) and basic sanity checks.

Data Management

* Always have backups, at a minimum avaiable in two independent locations
* Build a system for copying sanitised production data to other environments, optionally sampled to be usable in local development environments.
* Use the backups and sanitisation system to test backups regularly

Infrastructure Management

* Bake in HTTPS support immediately, even for local development environments.
* Have all infrastructure managed by one of the configuration management tools available e.g. Ansible, Terraform, etc.
* Always automate renewal of every HTTPS certificate used.
* Avoid anything that cannot be renewed automatically.
* For anything that cannot be automated and you have no choice, make sure renewal is due on a sane date and time.

Secrets

Miscellaneous

* Use an email provider that allows for quick creation of group or alias emails with permissions that can be assigned to multiple people.
* Use a group email for contact details to any provider no matter how sensitive.