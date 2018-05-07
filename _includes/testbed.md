{% assign testbed = page %}

# Testbed: {{ testbed.name }}

[Web site]({{testbed.www}})

## Description
{{ testbed.description }}

## Results for {{ testbed.name }}

|  | {% for protocol in site.protocols %} {{ protocol.name }} | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for profile in site.profiles %}
| [{{profile.name}}](/profiles/{{profile.title}}) |
{%- for protocol in site.protocols -%}
{%- assign cell_setups = site.setups | where: "profile", profile.title | where: "protocol": protocol.title | where: "testbed", testbed.title -%}
{%- for setup in cell_setups -%}
- [{{setup.name}}](/setups/{{setup.title}})<br/>
{%- endfor -%}
 |
{%- endfor -%}
{%- endfor %}
