{% assign run = page %}
{% include plotly/header.md %}

# Run page

## About the run

* Date: {{ run.date }}
* Label: {{ run.label }}
* Repository: [{{ run.repository }}](https://github.com/{{run.repository}})
* Branch: [{{ run.branch }}](https://github.com/{{run.repository}}/tree/{{run.branch}})
* Git commit: [{{ run.commit }}](https://github.com/{{run.repository}}/tree/{{run.commit}})

## Statistics summary

* End-to-end PDR: {{run.global-stats.pdr}} % *({{run.global-stats.packets-received}}/{{run.global-stats.packets-sent}} packets, or a loss rate of {{run.global-stats.loss-rate}})*
* Round-trip latency: {{run.global-stats.latency}} seconds
* Radio duty cycle: {{run.global-stats.duty-cycle}} %
* Channel utilization: {{run.global-stats.channel-utilization}} %
* Network formation time: {{run.global-stats.network-formation-time}} seconds

## Charts

{% for s in run.stats %}
{% assign metric = s[0] %}
* {{run.stats[metric].name}}

{% assign plot-id = {{forloop.index}} | append: "-per-node" %}
{% assign plot-xdata = {{run.stats[metric].per-node.x}} %}
{% assign plot-ydata = {{run.stats[metric].per-node.y}} %}
{% include plotly/barplot.md width=400 height=250 xlabel="Node" ylabel="" inline=true %}

{% assign plot-id = {{forloop.index}} | append: "-per-time" %}
{% assign plot-xdata = {{run.stats[metric].per-time.x}} %}
{% assign plot-ydata = {{run.stats[metric].per-time.y}} %}
{% include plotly/lineplot.md width=400 height=250 xlabel="Time (2-minute chunks)" ylabel="" inline=true %}

{% include plotly/boxplot-inline-clear.md %}

{% endfor %}
