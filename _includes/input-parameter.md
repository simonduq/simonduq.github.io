{% assign parameter = page %}

# Input Parameter: {{ parameter.name }}

{{ parameter.description }}

{% assign selected_profiles = "" | split: "" %}

{% for profile in site.profiles %}
{% if profile.input-parameters.traffic-pattern %}
{% assign selected_profiles = selected_profiles| push: profile %}
{% endif %}
{% endfor %}

{% assign selected_profiles_count = selected_profiles | size %}
{% if selected_profiles_count != 0 %}

This input parameter is used by the following profiles:
{% for profile in selected_profiles %}
* [{{ profile.name }}](/profiles/{{profile.uid}})
{% endfor %}

{% else %}
This input parameter is not currently used by any profile.
{% endif %}
