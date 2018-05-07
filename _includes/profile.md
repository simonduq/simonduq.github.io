{% assign profile = page %}

# Profile: {{ profile.name }}

## Description
{{ profile.description }}

## Metrics

{% if profile.input-parameters == None %}
None
{% else %}
{% for i in profile.input-parameters %}
{%- assign parameter = site.metrics | where: "title", i[0] | first -%}
* [{{ parameter.name }}](/metrics/input/{{i[0]}}): {{ i[1] }}
{% endfor %}
{% endif %}

## Observed Metrics

{% if profile.observed-metrics | size == 0 %}
None
{% else %}
{% for i in profile.observed-metrics %}
{%- assign metric = site.metrics | where: "title", i | first -%}
* [{{ metric.name }}](/metrics/observed/{{i}})
{% endfor %}
{% endif %}

## Output Metrics

{% if profile.output-metrics == None %}
None
{% else %}
{% for i in profile.output-metrics %}
{%- assign metric = site.metrics | where: "title", i | first -%}
* [{{ metric.name }}](/metrics/output/{{i}})
{% endfor %}
{% endif %}

## Results

{% include results-profile.md %}
