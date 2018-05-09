{% assign testbed = page %}

# Testbed: {{ testbed.name }}

[Web site]({{testbed.www}})

## Description
{{ testbed.description }}

## Results for {{ testbed.name }}

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
