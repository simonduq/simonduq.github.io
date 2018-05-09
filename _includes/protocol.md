{% assign protocol = page %}

# Protocol: {{ protocol.name }}

## Description
{{ page.description }}

## Results for {{ protocol.name }}

|  | {% for testbed in site.testbeds %} [{{testbed.name}}](/testbeds/{{testbed.title}}) | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for profile in site.profiles %}
| [{{profile.name}}](/profiles/{{profile.title}}) |
{%- for testbed in site.testbeds -%}
{%- assign cell_setups = site.setups | where: "profile", profile.title | where: "protocol": protocol.title | where: "testbed", testbed.title -%}
{%- for setup in cell_setups -%}
{%- assign profile = site.profiles | where: "title", setup.profile | first -%}
[[{{setup.configuration}}]](/setups/{{setup.title}})<br />
{%- endfor -%}
 |
{%- endfor -%}
{%- endfor %}
