[//]: # Computes mean on an array.
[//]: # Input: variable data, the array
[//]: # Return: variable return

{% assign sum__ = 0. %}
{% for val in data %}
{% assign sum__ = sum__ | plus: val %}
{% endfor %}
{% assign count__ = data | size %}
{% assign return = sum__ | divided_by: count__ %}
