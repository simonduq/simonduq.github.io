[//]: # Add one new x item to current botplot. Data taken from plot-ydata.
[//]: # Include parameters: name (x item label)

<script>

data.push({
  y: [
	{%- for yd in {{plot-ydata}} -%}
	  '{{yd}}',
	{%- endfor -%}
	],
  type: 'box',
	name: '{{include.name}}',
  marker: {
    color: 'rgb(8,81,156)',
  },
})

</script>
