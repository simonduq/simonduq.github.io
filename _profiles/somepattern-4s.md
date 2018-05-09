---
title: somepattern-4s
name: A given pattern, 4s
description: >
  This is a *markdown* description of the profile.
  Multiple lines are allowed, and so are:
    * Item lists
    * And basically any other markdown stuff.
input-parameters:
  traffic-pattern: Some pattern (space domain)
  traffic-period: 4s
  traffic-payload: 8B
observed-metrics: []
output-metrics: [ e2e-pdr, e2e-latency, power, link-prr ]
---

{% include profile.md %}
