{% include plotly/header.md %}
{% assign setup = page %}
{% assign runs = site.runs | where: "setup", setup.uid %}
{% assign runs = (runs | sort: "date") | reverse %}
{% assign runs_count = runs | size %}

# Setup page

## About the setup

* Label: {{ setup.label }}
{% if setup.repository %}
* Repository: [{{ setup.repository }}](https://github.com/{{setup.repository}})
* Branch: [{{ setup.branch }}](https://github.com/{{setup.repository}}/tree/{{setup.branch}})
* Path: [{{ setup.xppath }}](https://github.com/{{setup.repository}}/tree/{{setup.branch}}/{{setup.xppath}})
* Configuration: [{{ setup.configuration }}](https://github.com/{{setup.repository}}/tree/{{setup.branch}}/{{setup.xppath}}/Makefile)
{% endif %}

{{setup.description}}

## Statistics summary

[//]: # Compute mean statistics for this setup

{% assign duration_array = "" | split: "" %}
{% assign pdr_array = "" | split: "" %}
{% assign latency_array = "" | split: "" %}
{% assign duty_cycle_array = "" | split: "" %}
{% assign channel_utilization_array = "" | split: "" %}
{% assign network_formation_array = "" | split: "" %}

{% for run in runs %}
{% assign duration_array = duration_array | push: run.duration %}
{% assign pdr_array = pdr_array | push: run.global-stats.pdr %}
{% assign latency_array = latency_array | push: run.global-stats.latency %}
{% assign duty_cycle_array = duty_cycle_array | push: run.global-stats.duty-cycle %}
{% assign channel_utilization_array = channel_utilization_array | push: run.global-stats.channel-utilization %}
{% assign network_formation_array = network_formation_array | push: run.global-stats.network-formation-time %}
{% endfor %}

{% assign data = duration_array %}
{% include functions/mean.md %}
{% assign duration_mean = return %}

{% assign data = pdr_array %}
{% include functions/mean.md %}
{% assign pdr_mean = return %}

{% assign data = latency_array %}
{% include functions/mean.md %}
{% assign latency_mean = return %}

{% assign data = duty_cycle_array %}
{% include functions/mean.md %}
{% assign duty_cycle_mean = return %}

{% assign data = channel_utilization_array %}
{% include functions/mean.md %}
{% assign channel_utilization_mean = return %}

{% assign data = network_formation_array %}
{% include functions/mean.md %}
{% assign network_formation_mean = return %}

* Run duration: {{duration_mean}} minutes
* End-to-end PDR: {{pdr_mean}} %
* Round-trip latency: {{latency_mean}} seconds
* Radio duty cycle: {{duty_cycle_mean}} %
* Channel utilization: {{channel_utilization_mean}} %
* Network formation time: {{network_formation_mean}} seconds

## Runs

{% if runs_count != 0 %}

Runs for this setup:

|  | PDR (%) | RTT (s) | Duty cycle (%) |
| --- | ---: | ---: | ---:  |
{% for run in runs -%}
[{{run.date}}]({{ run.url }}) | {{run.global-stats.pdr}} | {{run.global-stats.latency}} | {{run.global-stats.duty-cycle}} |
{% endfor %}

## Graphs

{% for s in runs[0].stats %}
{% assign metric = s[0] %}
* {{runs[0].stats[metric].name}}

[//]: # Start new plot
{% assign plot-id = "summary-"| append: {{metric}} %}
{% include plotly/boxplot-init.md %}

[//]: # Add each run to the boxplot
{% for run in runs -%}

[//]: # Add data to boxplot (one new x item)
{% assign plot-ydata = run.stats[metric].per-node.y %}
{% assign date = run.date | date: "%m/%d/%Y %H:%M:%S" %}
{% include plotly/boxplot-add.md name=date %}

{% endfor %}

[//]: # Now, plot the current metric
{% include plotly/boxplot-show.md %}

{% endfor %}

{% else %}

No run for this setup.

{% endif %}
