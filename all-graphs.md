# All graphs for Develop branch

{% include plotly/header.md %}
{% assign develop_runs = site.runs | where_exp: "item", "item.branch!='contiki-ng/contiki-ng/develop'" %}
{% assign develop_runs = (develop_runs | sort: "date") | reverse %}

{% for s in develop_runs[0].stats %}
{% assign metric = s[0] %}
* {{develop_runs[0].stats[metric].name}}

[//]: # Start new plot
{% assign plot-id = "summary-"| append: {{metric}} %}
{% include plotly/boxplot-init.md %}

[//]: # Add each run to the boxplot
{% for run in develop_runs -%}

[//]: # Add data to boxplot (one new x item)
{% assign plot-ydata = run.stats[metric].per-node.y %}
{% assign date = run.date | date: "%m/%d/%Y %H:%M:%S" %}
{% include plotly/boxplot-add.md name=date %}

{% endfor %}

[//]: # Now, plot the current metric
{% include plotly/boxplot-show.md %}

{% endfor %}
