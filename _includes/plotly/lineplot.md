[//]: # Creates a plotly barplot into HTML div plot-id. Uses plot-xdata
[//]: # and plot-ydata as data sources. Include parameters: xlabel, ylabel

<span id='{{plot-id}}' {% if include.inline %} class='inline-plotly' {% endif %} ></span>

<script>

var data = [{
  x: [
{%- for xd in {{plot-xdata}} -%}
  '{{xd}}',
{%- endfor -%}
  ],
  y: [
{%- for yd in {{plot-ydata}} -%}
  {{yd}},
{%- endfor -%}
  ],
  type: 'line'
}];

var layout = {
  xaxis: {
    title: '{{ include.xlabel }}',
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
      r: 10,
      b: 40,
      t: 30,
      pad: 0,
    },
};

Plotly.newPlot('{{plot-id}}', data, layout);

</script>
