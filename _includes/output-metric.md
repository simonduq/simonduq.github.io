{% assign metric = page %}

# Output Metric: {{ metric.name }}

{{ metric.description }}

{% assign selected_profiles = site.profiles | where: "output-metrics", metric.title %}
{% assign selected_profiles_count = selected_profiles | size %}

{% if selected_profiles_count != 0 %}

This output metric is used by the following profiles:
{% for profile in selected_profiles %}
* [{{ profile.name }}](/profiles/{{profile.title}})
{% endfor %}

{% else %}
This output metric is not currently used by any profile.
{% endif %}
