{% assign metric = page %}

# Observed Metric: {{ metric.name }}

{{ metric.description }}

{% assign selected_profiles = site.profiles | where: "observed-metrics", metric.title %}
{% assign selected_profiles_count = selected_profiles | size %}

{% if selected_profiles_count != 0 %}

This observed metric is used by the following profiles:
{% for profile in selected_profiles %}
* [{{ profile.name }}](/profiles/{{profile.title}})
{% endfor %}

{% else %}
This observed metric is not currently used by any profile.
{% endif %}
