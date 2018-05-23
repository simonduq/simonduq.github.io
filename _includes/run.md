{% include plotly/header.md %}

{% assign run = page %}
{% assign setup = site.setups | where: "uid", run.setup | first %}

{% if setup.repository %}
{% assign label = setup.label %}
{% assign repository = setup.repository %}
{% assign branch = setup.branch %}
{% assign xppath = setup.xppath %}
{% assign flags = setup.flags %}
{% else %}
{% assign label = run.label %}
{% assign repository = run.repository %}
{% assign branch = run.branch %}
{% assign xppath = run.xppath %}
{% assign flags = run.flags %}
{% endif %}

# Run page

## About the run
* Label: {{label}}
* Date: {{ run.date | date: "%m/%d/%Y %H:%M:%S" }}
* Setup: [{{ run.setup }}]({{setup.url}})
* Repository: [{{ repository }}](https://github.com/{{repository}})
* Branch: [{{ branch }}](https://github.com/{{repository}}/tree/{{branch}})
* Path: [{{ xppath }}](https://github.com/{{repository}}/tree/{{branch}}/{{xppath}})
* Flags: [{{ flags }}](https://github.com/{{repository}}/tree/{{branch}}/{{xppath}}/Makefile)
* Git commit: [{{ run.commit }}](https://github.com/{{repository}}/tree/{{run.commit}})

Raw logs available at [{{run.title}}.txt](/logs/{{run.title}}.txt)

## Statistics summary

* Run duration: {{run.duration}} minutes
* Round-trip PDR: {{run.global-stats.pdr}} % *({{run.global-stats.packets-received}}/{{run.global-stats.packets-sent}} packets, or a loss rate of {{run.global-stats.loss-rate}})*
* Round-trip latency: {{run.global-stats.latency}} seconds
* Radio duty cycle: {{run.global-stats.duty-cycle}} %
* Channel utilization: {{run.global-stats.channel-utilization}} %
* Network formation time: {{run.global-stats.network-formation-time}} seconds

## Charts

{% for s in run.stats %}
{% assign metric = s[0] %}
* {{run.stats[metric].name}}:

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
