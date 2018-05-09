{% assign profile = page %}

# Profile: {{ profile.name }}

## Description
{{ profile.description }}

## Input Parameters

{% if profile.input-parameters == None %}
None
{% else %}
{% for i in profile.input-parameters %}
{%- assign parameter = site.metrics | where: "title", i[0] | first -%}
* [{{ parameter.name }}](/metrics/{{i[0]}}): {{ i[1] }}
{% endfor %}
{% endif %}

## Observed Metrics

{% if profile.observed-metrics | size == 0 %}
None
{% else %}
{% for i in profile.observed-metrics %}
{%- assign metric = site.metrics | where: "title", i | first -%}
* [{{ metric.name }}](/metrics/{{i}})
{% endfor %}
{% endif %}

## Output Metrics

{% if profile.output-metrics == None %}
None
{% else %}
{% for i in profile.output-metrics %}
{%- assign metric = site.metrics | where: "title", i | first -%}
* [{{ metric.name }}](/metrics/{{i}})
{% endfor %}
{% endif %}

## Results

{% assign profile_setups = site.setups | where: "profile", profile.title %}
{% assign profile_setups = profile_setups | sort: "testbed" %}

This profile has results for the following setups:
{%- for setup in profile_setups %}
{%- assign protocol = site.protocols | where: "title", setup.protocol | first %}
{%- assign testbed = site.testbeds | where: "title", setup.testbed | first %}
* [{{ protocol.name }} [{{ setup.configuration }}]. {{ profile.name }} @ {{ testbed.name }}](/setups/{{setup.title}})
{%- endfor %}

The data, with for each setup a distribution of per-run means, is shown next.

{% include plotly/header.md %}

{% for m in profile.output-metrics %}
{% assign metric = site.metrics | where: "title", m | first %}

{% comment %}
    For each metric plot performance of each setup.
    For each setup, we construct an array with one element
    per run, which contains the mean value over the run.
    The boxplot will show the distribution across runs in a given setup.
{% endcomment %}

{% assign plot-id = "summary-"| append: {{metric.title}} %}
{% include plotly/boxplot-init.md %}

{% for setup in profile_setups %}

{% assign protocol = site.protocols | where: "title", setup.protocol | first %}
{% assign testbed = site.testbeds | where: "title", setup.testbed | first %}
{% assign results = site.data.results[{{setup.title}}]}} %}
{% assign setup_name = {{protocol.name}} | append: " [" | append: {{setup.configuration}} | append: "]<br />" | append: {{testbed.name}}  %}
{% assign setup_means = "" | split: "" %}

{% for run in results %}

{% assign data = run[1][metric.title] %}
{% include functions/mean.md %}
{% assign setup_means = setup_means | push: return %}

{% endfor %}

{% assign plot-ydata = setup_means %}
{% include plotly/boxplot-add.md name=setup_name %}

{% endfor %}

{% comment %}
    Now, plot the current metric
{% endcomment %}

{% include plotly/boxplot-show.md ylabel=metric.name %}

{% endfor %}
