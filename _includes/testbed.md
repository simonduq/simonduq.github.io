[//]: # Meant for inclusion from pages under \_testbeds, which defines
[//]: # testbeds. Shows a description of the testbed and lists associated
[//]: # results in a table.

{% assign testbed = page %}

# Testbed: {{ testbed.name }}

[Web site]({{testbed.www}})

## Description
{{ testbed.description }}

## Results for {{ testbed.name }}

[//]: # Build a table with one row per profile, one column per protocol,
[//]: # and each cell showing all setups with results for this testbed.

|  | {% for protocol in site.protocols %} [{{protocol.name}}](/protocols/{{protocol.uid}}) | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for profile in site.profiles %}
| [{{profile.name}}](/profiles/{{profile.uid}}) |
{%- for protocol in site.protocols -%}
{%- assign cell_setups = site.setups | where: "profile", profile.uid | where: "protocol": protocol.uid | where: "testbed", testbed.uid -%}
{%- for setup in cell_setups -%}
{%- assign profile = site.profiles | where: "uid", setup.profile | first -%}
[[{{setup.configuration}}]](/setups/{{setup.uid}})<br />
{%- endfor -%}
 |
{%- endfor -%}
{%- endfor %}
