{% assign setup = page %}
{% assign profile = site.profiles | where: "title", setup.profile | first %}
{% assign testbed = site.testbeds | where: "title", setup.testbed | first %}
{% assign protocol = site.protocols | where: "title", setup.protocol | first %}

# Setup: {{ setup.name }}

## Setup

This page will include results for:
* Profile: [{{profile.name}}](/profiles/{{profile.title}})
* Testbed: [{{testbed.name}}](/testbeds/{{testbed.title}})
* Protocol: [{{protocol.name}}](/protocols/{{protocol.title}})

{{setup.description}}

## Results for {{ setup.name }}

|  | {% for protocol in site.protocols %} {{ protocol.name }} | {% endfor %}
| --- | {% for setup in site.setups %} --- | {% endfor %}
{%- for profile in site.profiles %}
| [{{profile.name}}](/profiles/{{profile.title}}) |
{%- for protocol in site.protocols -%}
{%- if setup.protocol == protocol.title and setup.profile == profile.title -%}
  [Results](TODO) |
{%- endif -%}
{%- endfor -%}
{%- endfor %}

## Resources

Available resources:
* Source code: TODO
* RAW logs: TODO
* Processing scripts: TODO
* Usage instructions: TODO
