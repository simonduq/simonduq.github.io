[//]: # Meant for inclusion from pages under \_metrics/observed, which defines
[//]: # observed metrics.

{% assign metric = page %}

# Observed Metric: {{ metric.name }}

{{ metric.description }}

[//]: # Extrat and list all profiles that use this metric.
{% assign selected_profiles = site.profiles | where: "observed-metrics", metric.uid %}
{% assign selected_profiles_count = selected_profiles | size %}

{% if selected_profiles_count != 0 %}

This observed metric is used by the following profiles:
{% for profile in selected_profiles %}
* [{{ profile.name }}](/profiles/{{profile.uid}})
{% endfor %}

{% else %}
This observed metric is not currently used by any profile.
{% endif %}
