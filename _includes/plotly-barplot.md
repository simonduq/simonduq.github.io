<div id='{{plot-id}}'></div>

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
  type: 'bar'
}];

var layout = {
  xaxis: {
    title: '{{ include.xlabel }}',
  },
  yaxis: {
    title: '{{ include.ylabel }}',
  },
};

Plotly.newPlot('{{plot-id}}', data, layout);

</script>
