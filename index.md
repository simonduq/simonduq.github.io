# Home Page

Welcome to the IoT-Bench repository.
This repository defines the framework for profiles, as well as a set of profiles and associated results.


The general IoT-Bench website is at: [www.iotbench.ethz.ch](https://www.iotbench.ethz.ch)

## Profile Framework

The general IoT-Bench framework can be found [here](pages/framework).

## Profiles

We currently have the following profiles:
{% for profile in site.profiles %}
* [{{profile.name}}](profiles/{{profile.title}})
{% endfor %}

[This page](pages/results-per-profile.html) summarizes all evaluation results, shown per-profile.

## Testbeds

We currently have the following testbeds:
{% for testbed in site.testbeds %}
* [{{testbed.name}}](testbeds/{{testbed.title}})
{% endfor %}

## Protocols

We currently have results for the following protocols:
{% for protocol in site.protocols %}
* [{{protocol.name}}](protocols/{{protocol.title}})
{% endfor %}
