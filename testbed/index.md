# Home Page

{% include plotly/header.md %}
{% assign develop_runs = site.runs | where_exp: "item", "item.branch!='contiki-ng/contiki-ng/develop'" %}
{% assign develop_runs = (develop_runs | sort: "date") | reverse %}
{% assign other_runs = site.runs | where_exp: "item", "item.branch=='contiki-ng/contiki-ng/develop'" %}
{% assign other_runs = (other_runs | sort: "date") | reverse %}

## Contiki-NG 'develop' branch

{% assign develop_runs_count = develop_runs | size %}
{% if develop_runs_count != 0 %}
|  | PDR (%) | RTT (s) | Duty cycle (%) |
| --- | ---: | ---: | ---:  |
{% for run in develop_runs -%}
[{{run.label}} -- {{run.date}}]({{ run.url }}) | {{run.global-stats.pdr}} | {{run.global-stats.latency}} | {{run.global-stats.duty-cycle}} |
{% endfor %}
{% endif %}

[//]: # Plot PDR for all runs of the the develop branch
{% assign metric = "pdr" %}
{% assign plot-id = "summary-"| append: {{metric}} %}
{% include plotly/boxplot-init.md %}

{% for run in develop_runs -%}
[//]: # Add data to boxplot (one new x item)
{% assign plot-ydata = run.stats[metric].per-node.y %}
{% assign date = run.date | date: "%m/%d/%Y %H:%M:%S" %}
{% include plotly/boxplot-add.md name=date %}
{% endfor %}

[//]: # Now, plot the current boxplot
{% include plotly/boxplot-show.md ylabel="End-to-end PDR (%)"%}

More graphs available on [this page](all-graphs).

## Other runs

{% assign other_runs_count = other_runs | size %}
{% if other_runs_count != 0 %}
|  | PDR (%) | RTT (s) | Duty cycle (%) |
| --- | ---: | ---: | ---:  |
{% for run in other_runs -%}
[{{run.label}} -- {{run.date}}]({{ run.url }}) | {{run.global-stats.pdr}} | {{run.global-stats.latency}} | {{run.global-stats.duty-cycle}} |
{% endfor %}
{% endif %}
