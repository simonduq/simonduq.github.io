---
uid: somepattern-random
name: A given pattern, 1--180s
description: >
  This is a *markdown* description of the profile.
  Multiple lines are allowed, and so are:
    * Item lists
    * And basically any other markdown stuff.
input-parameters:
  traffic-pattern: Some pattern (space domain)
  traffic-period: 1s--180s
  traffic-payload: 4B-1kB
observed-metrics: []
output-metrics: [ e2e-pdr, e2e-latency, power ]
---

{% include profile.md %}
