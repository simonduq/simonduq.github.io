[//]: # Computes weighted mean on an array.
[//]: # Input: variable data, the array, and data_weights, the weights
[//]: # Return: variable return

{% assign sum__ = 0. %}
{% assign sum_weights__ = 0. %}
{% for val in {{data}} %}
{% assign index = forloop.index | plus: -1 %}
{% assign w = data_weights[index] %}
{% assign sum_weights__ = sum_weights__ | plus: w %}
{% assign valw = val | times: w %}
{% assign sum__ = sum__ | plus: valw %}
{% endfor %}
{% assign return = sum__ | divided_by: sum_weights__ %}
