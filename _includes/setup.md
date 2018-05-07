{% assign setup = page %}
{% assign profile = site.profiles | where: "title", setup.profile | first %}
{% assign testbed = site.testbeds | where: "title", setup.testbed | first %}
{% assign protocol = site.protocols | where: "title", setup.protocol | first %}

# Setup: {{ protocol.name }} [{{ setup.configuration }}]. {{ profile.name }} {{ testbed.name }}

This page shows the following setup:
* Profile: [{{profile.name}}](/profiles/{{profile.title}})
* Testbed: [{{testbed.name}}](/testbeds/{{testbed.title}})
* Protocol: [{{protocol.name}}](/protocols/{{protocol.title}})
* Configuration: {{ setup.configuration }}

{{setup.description}}

## Resources

Available resources:
* Source code: TODO
* RAW logs: TODO
* Processing scripts: TODO
* Usage instructions: TODO

## Results

{% include results-setup.md %}
