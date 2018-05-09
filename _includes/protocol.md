{% assign protocol = page %}

# Protocol: {{ protocol.name }}

## Description
{{ page.description }}

## Results for {{ protocol.name }}

|  | {% for testbed in site.testbeds %} [{{testbed.name}}](/testbeds/{{testbed.uid}}) | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for profile in site.profiles %}
| [{{profile.name}}](/profiles/{{profile.uid}}) |
{%- for testbed in site.testbeds -%}
{%- assign cell_setups = site.setups | where: "profile", profile.uid | where: "protocol": protocol.uid | where: "testbed", testbed.uid -%}
{%- for setup in cell_setups -%}
{%- assign profile = site.profiles | where: "uid", setup.profile | first -%}
[[{{setup.configuration}}]](/setups/{{setup.uid}})<br />
{%- endfor -%}
 |
{%- endfor -%}
{%- endfor %}
