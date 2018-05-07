{% assign profile_setups = site.setups | where: "profile", profile.title %}
{% assign profile_setups = profile_setups | sort: "testbed" %}

This profile has results for the following setups:
{%- for setup in profile_setups %}
{%- assign protocol = site.protocols | where: "title", setup.protocol | first %}
{%- assign testbed = site.testbeds | where: "title", setup.testbed | first %}
* [{{setup.title}}: {{ protocol.name }} [{{ setup.configuration }}]. {{ profile.name }} {{ testbed.name }}](/setups/{{setup.title}})
{%- endfor %}

{% include d3-barplot-header.md %}
<div id="chart-summary"></div>

{% comment %}
    For each metric: compute per-setup average across runs
{% endcomment %}

{% for m in profile.output-metrics %}
{% assign metric = site.metrics | where: "title", m | first %}

{% assign profile_keys = "" | split: "" %}
{% assign profile_means = "" | split: "" %}

{% for s in profile_setups %}

{% assign results = site.data.results[{{s.title}}]}} %}
{% assign setup_keys = "" | split: "" %}
{% assign setup_means = "" | split: "" %}

{% for run in results %}

{% assign data = run[1][metric.title] %}
{% include function-mean.md %}
{% assign setup_means = setup_means | push: return %}
{% assign setup_keys = setup_keys | push: run[0] %}

{% endfor %}

{% assign data = setup_means %}
{% include function-mean.md %}
{% assign profile_means = profile_means | push: return %}
{% assign profile_keys = profile_keys | push: s.title %}

{% endfor %}

{% comment %}
    Now, plot
{% endcomment %}

{% assign plot-xdata = profile_keys %}
{% assign plot-ydata = profile_means %}
{% include d3-barplot.md id="chart-summary" xlabel="" ylabel=metric.name ymax=metric.ymax %}

{% endfor %}
