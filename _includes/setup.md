{% assign setup = page %}
{% assign profile = site.profiles | where: "uid", setup.profile | first %}
{% assign testbed = site.testbeds | where: "uid", setup.testbed | first %}
{% assign protocol = site.protocols | where: "uid", setup.protocol | first %}

# Setup: {{ protocol.name }} [{{ setup.configuration }}]. {{ profile.name }} @ {{ testbed.name }}

This page shows the following setup:
* Profile: [{{profile.name}}](/profiles/{{profile.uid}})
* Testbed: [{{testbed.name}}](/testbeds/{{testbed.uid}})
* Protocol: [{{protocol.name}}](/protocols/{{protocol.uid}})
* Configuration: {{ setup.configuration }}

{{setup.description}}

## Resources

Available resources:
* Source code: TODO
* RAW logs: TODO
* Processing scripts: TODO
* Usage instructions: TODO

## Results

{% assign results = site.data.results[{{setup.uid}}]}} %}

{% include plotly/header.md %}

### Results Summary

{% for m in profile.output-metrics %}

{% assign metric = site.metrics | where: "uid", m | first %}

{% assign setup_keys = "" | split: "" %}
{% assign setup_means = "" | split: "" %}

{% assign plot-id  = "summary-" | append: {{metric.uid}} %}
{% include plotly/boxplot-init.md %}

{% for run in results %}

{% assign run_name = run[0] %}
{% assign data = run[1][metric.uid] %}

{% assign setup_keys = setup_keys | push: run[0] %}
{% assign setup_means = setup_means | push: return %}

{% assign plot-ydata = run[1][metric.uid] %}
{% include plotly/boxplot-add.md name=run_name %}

{% endfor %}

{% include plotly/boxplot-show.md ylabel=metric.name %}

{% endfor %}

### Per-run Results

{% for run in results %}
{% assign runid = run[0] %}
{% assign res = results[{{runid}}] %}

#### {{runid}}

{% for m in profile.output-metrics %}
{% assign metric = site.metrics | where: "uid", m | first %}

{% assign plot-id = {{runid}} | append: {{metric.uid}} %}
{% include plotly/boxplot-init.md inline=true %}
{% assign plot-ydata = res[metric.uid] %}
{% include plotly/boxplot-add.md %}
{% include plotly/boxplot-show.md name=" " width=200 height=200 name="Dist" xaxis=false ylabel=metric.name %}

{% endfor %}

{% include plotly/boxplot-inline-clear.md %}

{% endfor %}
