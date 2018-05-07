<script>

var svg = d3.select("#{{include.id}}").append("svg:svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

svg.call(tip);

var data = [
{%- for xd in {{plot-xdata}} %}
{%- assign index = forloop.index | minus: 1 %}
             { x: "{{xd}}", y: {{plot-ydata[index]}} },
{%- endfor %}
             ]
d3.select(window).on("load", do_plot(svg, data, "{{include.xlabel}}", "{{include.ylabel}}", "{{include.ymax}}"));

</script>
