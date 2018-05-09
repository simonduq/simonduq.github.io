{% assign results = site.data.results[{{setup.title}}]}} %}

{% include plotly-header.md %}

### Results Summary

{% for m in profile.output-metrics %}

{% assign metric = site.metrics | where: "title", m | first %}

{% assign setup_keys = "" | split: "" %}
{% assign setup_means = "" | split: "" %}

{% assign plot-id  = "summary-" | append: {{metric.title}} %}
{% include plotly-boxplot-init.md %}

{% for run in results %}

{% assign run_name = run[0] %}
{% assign data = run[1][metric.title] %}

{% assign setup_keys = setup_keys | push: run[0] %}
{% assign setup_means = setup_means | push: return %}

{% assign plot-ydata = run[1][metric.title] %}
{% include plotly-boxplot-add.md name=run_name %}

{% endfor %}

{% include plotly-boxplot-show.md ylabel=metric.name %}

{% endfor %}

### Per-run Results

{% for run in results %}
{% assign runid = run[0] %}
{% assign res = results[{{runid}}] %}

#### {{runid}}

{% for m in profile.output-metrics %}
{% assign metric = site.metrics | where: "title", m | first %}

{% assign plot-id = {{runid}} | append: {{metric.title}} %}
{% include plotly-boxplot-init.md inline=true %}
{% assign plot-ydata = res[metric.title] %}
{% include plotly-boxplot-add.md %}
{% include plotly-boxplot-show.md name=" " width=200 height=200 name="Dist" xaxis=false ylabel=metric.name %}

{% endfor %}

{% include plotly-boxplot-inline-clear.md %}

{% endfor %}
