{% if meta.onshape %}

# {{ meta.title }}

{% block header %}
{% endblock header %}

![preview](assets/{{meta.onshape.uid_slug}}.png)

## Description

{% block description %}
{% endblock description %}

{% include 'onshape/bom.md' %}

## Links

{{ cad_link }}

{% else %}
{% include 'onshape/meta_error.md' %}
{% endif %}
