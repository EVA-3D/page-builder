!!! error "Invalid meta data"

    To use this page template you need to configure the `onshape` page meta data, i.e.

    ```
    ---
    title: my page
    onshape:
        uid: EVA / Project / Mosquito
        cad_url: https://cad.onshape.com/
    ---
    {% raw %}
    {% extends 'onshape/page.md' %}
    {% endraw %}
    ```
