{% assign profile = page %}

# Profile: {{ page.name }}

## Description
{{ page.description }}

## Metrics

{% if page.input-parameters == None %}
None
{% else %}
{% for i in page.input-parameters %}
{%- assign parameter = site.metrics | where: "title", i[0] | first -%}
* [{{ parameter.name }}](/metrics/input/{{i[0]}}): {{ i[1] }}
{% endfor %}
{% endif %}

## Observed Metrics

{% if page.observed-metrics == None %}
None
{% else %}
{% for i in page.observed-metrics %}
{%- assign metric = site.metrics | where: "title", i | first -%}
* [{{ metric.name }}](/metrics/observed/{{i}})
{% endfor %}
{% endif %}

## Output Metrics

{% if page.output-metrics == None %}
None
{% else %}
{% for i in page.output-metrics %}
{%- assign metric = site.metrics | where: "title", i | first -%}
* [{{ metric.name }}](/metrics/output/{{i}})
{% endfor %}
{% endif %}

## Results

{% assign profile_setups = site.setups | where: "profile", profile.title %}
{% assign all_metrics = page.output-metrics | concat: page.observed-metrics %}

|  | {% for m in all_metrics %} {% assign metric = site.metrics | where: "title", m | first %} {{metric.name | truncate: 16 }} | {% endfor %}
| --- | {% for m in all_metrics %} --- | {% endfor %}
{%- for setup in profile_setups %}
{%- assign protocol = site.protocols | where: "title", setup.protocol | first %}
{%- assign testbed = site.testbeds | where: "title", setup.testbed | first %}
[{{setup.name}}](/setups/{{setup.title}}) ({{testbed.name}}, {{protocol.name}}) | | | |
{%- endfor %}
