---
title: How to post AppDynamics events to Datadog
kind: faq
customnav: developersnav
---

This article will allow you to submit events from your AppDynamics Application into your Datadog Event stream.  Please note that this plugin was written by the team at AppDynamics and is not currently supported by Datadog.  Should you encounter any issues please contact their team [here](https://www.appdynamics.com/support/)

Prerequisites: You must be running AppDynamics 4.1 or later

First, create DataDog Policy Single Violation Only HTTP Template:

```json
{
"title": "${latestEvent.displayName} - ${policy.name} ",
"text": "${latestEvent.summaryMessage} ${latestEvent.guid} ${latestEvent.eventTypeKey} Policy Name - ${policy.name} Policy ID - ${policy.id}  Policy Digest : ${policy.digest} ${policy.digestDurationInMins} ",
"alert_type":"${topSeverity}",
"priority":"${priority}",
"aggregation_key":" ${policy.id} ", 
"tags":["guid:${latestEvent.guid}","eventid:${latestEvent.id}","environment:${Environment}","os:${OS}","platform:${Platform}"] 
}
```

{{< img src="developers/faq/step_1_appdynamics.png" alt="step_1_appdynamics" responsive="true" >}}

Latest Event:
```json
{
"title": "${latestEvent.displayName}",
"text": "${latestEvent.summaryMessage} ${latestEvent.eventTypeKey}",
"alert_type":"${topSeverity}",
"priority":"${priority}",
"aggregation_key":"${latestEvent.guid}", "tags":["guid:${latestEvent.guid}","eventid:${latestEvent.id}","environment:${Environment}","os:${OS}","platform:${Platform}"] 
}
```

{{< img src="developers/faq/latest_event.png" alt="latest_event" responsive="true" >}}


You can use also use Email Templates:

```json
{
"title": "AppDynamicsEvent",
"text": "ApplicationChangeEvent",
"priority": "normal",
"tags": ["os:windows"],
"alert_type": "info"
}
```

{{< img src="developers/faq/email_template.png" alt="email_template" responsive="true" >}}