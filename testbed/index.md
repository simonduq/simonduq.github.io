# Home Page

{% include plotly/header.md %}

{% assign setups = (site.setups | sort: "index") %}
{% for setup in setups %}

## {{setup.label}}

{% assign runs = site.runs | where: "setup", setup.uid %}
{% assign runs = (runs | sort: "date") | reverse %}
{% assign runs_count = runs | size %}

{% if runs_count != 0 %}

For graphs and statistics summary, visit: [{{setup.uid}}]({{setup.url}}).

Runs for this setup:

|  | PDR (%) | RTT (s) | Duty cycle (%) |
| --- | ---: | ---: | ---:  |
{% for run in runs -%}
{% assign date = run.date | date: "%m/%d/%Y %H:%M:%S" -%}
[{{date}}]({{ run.url }}) | {{run.global-stats.pdr}} | {{run.global-stats.latency}} | {{run.global-stats.duty-cycle}} |
{% endfor %}

{% else %}

No run for this setup ([{{setup.uid}}]({{setup.url}})).

{% endif %}

{% endfor %}
