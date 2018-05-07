{% assign profile_setups = site.setups | where: "profile", profile.title %}
{% assign all_metrics = profile.output-metrics | concat: profile.observed-metrics %}

|  | {% for m in all_metrics %}
{%- assign metric = site.metrics | where: "title", m | first -%}
[{{metric.name | truncate: 16 }}](/metrics/{{metric.title}}) |
{%- endfor %}
| --- | {% for m in all_metrics %} ---: | {% endfor %}
{%- for setup in profile_setups %}
{%- assign protocol = site.protocols | where: "title", setup.protocol | first %}
{%- assign testbed = site.testbeds | where: "title", setup.testbed | first %}
[{{setup.name}}](/setups/{{setup.title}}) ({{testbed.name}}, {{protocol.name}}) |
{%- for m in all_metrics -%}
{{ site.data.results[setup.title][m]}} |
{%- endfor %}
{%- endfor %}
