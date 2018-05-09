---
uid: somepattern-50s
name: A given pattern, 50s
description: >
  This is a *markdown* description of the profile.
  Multiple lines are allowed, and so are:
    * Item lists
    * And basically any other markdown stuff.
input-parameters:
  traffic-pattern: Some pattern (space domain)
  traffic-period: 50s
  traffic-payload: 4B
observed-metrics: []
output-metrics: [ e2e-pdr, e2e-latency, power, channel-utilization ]
---

{% include profile.md %}
