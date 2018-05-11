[//]: # Meant for inclusion from pages under \_metrics/input, which defines
[//]: # input parameters.

{% assign parameter = page %}

# Input Parameter: {{ parameter.name }}

{{ parameter.description }}

{% assign selected_profiles = "" | split: "" %}

[//]: # Extract all profiles that make use of the input parameter
{% for profile in site.profiles %}
{% if profile.input-parameters.traffic-pattern %}
{% assign selected_profiles = selected_profiles| push: profile %}
{% endif %}
{% endfor %}

{% assign selected_profiles_count = selected_profiles | size %}
{% if selected_profiles_count != 0 %}

[//]: # List all selected profiles
This input parameter is used by the following profiles:
{% for profile in selected_profiles %}
* [{{ profile.name }}](/profiles/{{profile.uid}})
{% endfor %}

{% else %}
This input parameter is not currently used by any profile.
{% endif %}
