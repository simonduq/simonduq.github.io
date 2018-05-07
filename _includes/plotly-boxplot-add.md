<script>

data.push({
  y: [
	{%- for yd in {{plot-ydata}} -%}
	  '{{yd}}',
	{%- endfor -%}
	],
  type: 'box',
	name: '{{include.name}}',
})

</script>
