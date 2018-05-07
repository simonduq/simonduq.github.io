{% include plotly-header.md %}

{% assign plot-id = 'chart' %}
{% include plotly-boxplot-init.md %}

{% assign plot-ydata = site.data.results.setup1.run1.e2e-pdr %}
{% include plotly-boxplot-add.md name='run1' %}

{% assign plot-ydata = site.data.results.setup1.run2.e2e-pdr %}
{% include plotly-boxplot-add.md name='run2' %}

{% assign plot-ydata = site.data.results.setup1.run3.e2e-pdr %}
{% include plotly-boxplot-add.md name='run3' %}

{% include plotly-boxplot-show.md xlabel="Node" ylabel="PDR (%)" %}
