[//]: # Meant for inclusion from pages under \_setups, which defines
[//]: # experiment setups. Shows a textual description of the setup,
[//]: # as well as the profile, testbed, protocol, and configuration used.
[//]: # Then plots all results for this setup, including per-run details.

{% assign setup = page %}
{% assign profile = site.profiles | where: "uid", setup.profile | first %}
{% assign testbed = site.testbeds | where: "uid", setup.testbed | first %}
{% assign protocol = site.protocols | where: "uid", setup.protocol | first %}

# Experimental Setup page

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

[//]: # For each metric, build a boxplot showing the distribution of results
[//]: # across runs. One x item per run.

{% for m in profile.output-metrics %}

{% assign metric = site.metrics | where: "uid", m | first %}

{% assign setup_keys = "" | split: "" %}
[//]: # Create an array with mean metric value of each run.
{% assign setup_means = "" | split: "" %}

[//]: # Initialize boxplot
{% assign plot-id  = "summary-" | append: {{metric.uid}} %}
{% include plotly/boxplot-init.md %}

{% for run in results %}

{% assign run_name = run[0] %}
{% assign data = run[1][metric.uid] %}

[//]: # Collect x items for the plot: key and per-setup mean
{% assign setup_keys = setup_keys | push: run[0] %}
{% assign setup_means = setup_means | push: return %}

[//]: # Add x item to current boxplot
{% assign plot-ydata = run[1][metric.uid] %}
{% include plotly/boxplot-add.md name=run_name %}

{% endfor %}

[//]: # Finalize current boxplot
{% include plotly/boxplot-show.md ylabel=metric.name %}

{% endfor %}

### Per-run Results

[//]: # Now show per-run statistics

{% for run in results %}
{% assign runid = run[0] %}
{% assign res = results[{{runid}}] %}

* {{runid}} *({{run[1].date}})*

[//]: # For each metric, create a boxplot. Show the boxplots as HTML inline
[//]: # elements. The boxplot shows, for a given metric, the distribution
[//]: # of values reported for the run. Can be per-node or per-packet
[//]: # or even something else.

{% for m in profile.output-metrics %}
{% assign metric = site.metrics | where: "uid", m | first %}

[//]: # Plot current metric for current run
{% assign plot-id = {{runid}} | append: {{metric.uid}} %}
{% include plotly/boxplot-init.md inline=true %}
{% assign plot-ydata = res[metric.uid] %}
{% include plotly/boxplot-add.md %}
{% include plotly/boxplot-show.md name=" " width=200 height=200 name="Dist" xaxis=false ylabel=metric.name %}

{% endfor %}

[//]: # Done with this run, clear the inline elements before moving on to next run
{% include plotly/boxplot-inline-clear.md %}

{% endfor %}
