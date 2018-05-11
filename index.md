# Home Page

Welcome to the IoT-Bench repository.
This repository defines the framework for profiles, as well as a set of profiles and associated results.
To contribute new profiles or results, see our [Wiki](TODO).

The general IoT-Bench website is at: [www.iotbench.ethz.ch](https://www.iotbench.ethz.ch)

## Profile Framework

The general IoT-Bench framework can be found [here](/pages/framework).

## Profiles

We currently have the following profiles:
{% for profile in site.profiles %}
* [{{profile.name}}](/profiles/{{profile.uid}})
{% endfor %}

## Testbeds

We currently have the following testbeds:
{% for testbed in site.testbeds %}
* [{{testbed.name}}](/testbeds/{{testbed.uid}})
{% endfor %}

## Protocols

We currently have results for the following protocols:
{% for protocol in site.protocols %}
* [{{protocol.name}}](/protocols/{{protocol.uid}})
{% endfor %}

## Results

A summary of current results is shown below:

[//]: # Show a table one row per profile, one column per testbed, and in each
[//]: # cell, the setups we have results for.

|  | {% for testbed in site.testbeds %} [{{testbed.name}}](/testbeds/{{testbed.uid}}) | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for profile in site.profiles %}
| [{{profile.name}}](/profiles/{{profile.uid}}) |
{%- for testbed in site.testbeds -%}
{%- assign cell_setups = site.setups | where: "profile", profile.uid | where: "testbed", testbed.uid -%}
{%- for setup in cell_setups -%}
{%- assign protocol = site.protocols | where: "uid", setup.protocol | first -%}
{%- assign profile = site.profiles | where: "uid", setup.profile | first -%}
<small>[{{protocol.name}} [{{setup.configuration}}]](/setups/{{setup.uid}})</small><br />
{%- endfor -%}
 |
{%- endfor -%}
{%- endfor %}
