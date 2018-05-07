---
title: many2many-30s
name: Many-to-many, 30s
description: >
  This is a *markdown* description of the profile.
  Multiple lines are allowed, and so are:
    * Item lists
    * And basically any other markdown stuff.
input-parameters:
  traffic-pattern: Many-to-many
  traffic-period: 30s
  traffic-payload: 4B
observed-metrics: []
output-metrics: [ e2e-pdr, e2e-latency, power, channel-utilization ]
---

{% include profile.md %}
