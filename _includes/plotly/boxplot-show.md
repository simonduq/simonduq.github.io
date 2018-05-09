<script>

var layout = {
  xaxis: {
{%- if include.xaxis == false %}
    visible: false,
{%- endif %}
  },
  yaxis: {
    uid: '{{ include.ylabel }}',
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
    b: 40,
    t: 0,
    pad: 4,
  },
  showlegend: false,
};

Plotly.newPlot('{{plot-id}}', data, layout);

</script>
