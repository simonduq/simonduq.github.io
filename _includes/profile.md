[//]: # Meant for inclusion from pages under \_profiles, which defines
[//]: # evaluation profiles. Shows a description of the profile, i.e.
[//]: # textual, as well as assigned input parameters, and selected
[//]: # observed and output metrics. Also shows a table summary
[//]: # of all results for this profile. Finally, plots all results.

{% assign profile = page %}

# Profile: {{ profile.name }}

## Description
{{ profile.description }}

## Input Parameters

{% if profile.input-parameters == None %}
None
{% else %}
{% for i in profile.input-parameters %}
{%- assign parameter = site.metrics | where: "uid", i[0] | first -%}
* [{{ parameter.name }}](/metrics/{{i[0]}}): {{ i[1] }}
{% endfor %}
{% endif %}

## Observed Metrics

{% if profile.observed-metrics | size == 0 %}
None
{% else %}
{% for i in profile.observed-metrics %}
{%- assign metric = site.metrics | where: "uid", i | first -%}
* [{{ metric.name }}](/metrics/{{i}})
{% endfor %}
{% endif %}

## Output Metrics

{% if profile.output-metrics == None %}
None
{% else %}
{% for i in profile.output-metrics %}
{%- assign metric = site.metrics | where: "uid", i | first -%}
* [{{ metric.name }}](/metrics/{{i}})
{% endfor %}
{% endif %}

## Results

{% assign profile_setups = site.setups | where: "profile", profile.uid %}
{% assign profile_setups = profile_setups | sort: "testbed" %}

This profile has results for the following setups:

[//]: # Build a table with one row per protocol, one column per testbed,
[//]: # and each cell showing all setups with results for this profile.

|  | {% for testbed in site.testbeds %} [{{testbed.name}}](/testbeds/{{testbed.uid}}) | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for protocol in site.protocols %}
| [{{protocol.name}}](/protocols/{{protocol.uid}}) |
{%- for testbed in site.testbeds -%}
{%- assign cell_setups = site.setups | where: "profile", profile.uid | where: "protocol": protocol.uid | where: "testbed", testbed.uid -%}
{%- for setup in cell_setups -%}
{%- assign profile = site.profiles | where: "uid", setup.profile | first -%}
[[{{setup.configuration}}]](/setups/{{setup.uid}})<br />
{%- endfor -%}
 |
{%- endfor -%}
{%- endfor %}

The data, with for each setup a distribution of per-run means, is shown next.

{% include plotly/header.md %}

{% for m in profile.output-metrics %}
{% assign metric = site.metrics | where: "uid", m | first %}

[//]: # For each metric plot performance of each setup as a boxplot-init
[//]: # For each setup, we construct an array with one element
[//]: # per run, which contains the mean value over the run.
[//]: # The boxplot will show the distribution across runs in a given setup.
[//]: # One x item per setup.

[//]: # Start new plot
{% assign plot-id = "summary-"| append: {{metric.uid}} %}
{% include plotly/boxplot-init.md %}

[//]: # For each setup, build array that summarizes results for the current metric
{% for setup in profile_setups %}

{% assign protocol = site.protocols | where: "uid", setup.protocol | first %}
{% assign testbed = site.testbeds | where: "uid", setup.testbed | first %}
{% assign results = site.data.results[{{setup.uid}}]}} %}
{% assign setup_name = {{protocol.name}} | append: " [" | append: {{setup.configuration}} | append: "]<br />" | append: {{testbed.name}}  %}
[//]: # Create an empty array where to store the mean result of each run
{% assign setup_means = "" | split: "" %}

{% for run in results %}

[//]: # Compute mean metric for this run, populate array setup_means
{% assign data = run[1][metric.uid] %}
{% include functions/mean.md %}
{% assign setup_means = setup_means | push: return %}

{% endfor %}

[//]: # Add data to boxplot (one new x item)
{% assign plot-ydata = setup_means %}
{% include plotly/boxplot-add.md name=setup_name %}

{% endfor %}

[//]: # Now, plot the current metric
{% include plotly/boxplot-show.md ylabel=metric.name %}

{% endfor %}
