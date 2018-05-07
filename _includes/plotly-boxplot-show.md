<script>

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
