[//]: # Finalizes and creates the current boxplot into HTML div plot-id.
[//]: # Include parameters: width, height, ylabel.

<script>

var layout = {
  xaxis: {
{%- if include.xaxis == false %}
    visible: false,
{%- endif %}
  },
  yaxis: {
    title: '{{ include.ylabel }}',
  },
  autosize: false,

{%- if include.height %}
  height: {{ include.height }},
{%- else %}
  height: 300,
{%- endif %}
{%- if include.width %}
  width: {{ include.width }},
{%- endif %}
  margin: {
    l: 70,
    r: 0,
    b: 80,
    t: 30,
    pad: 0,
  },
  showlegend: false,
};

Plotly.newPlot('{{plot-id}}', data, layout);

</script>
