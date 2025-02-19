---
resource_types: all
datatype: "{<dictionary>}"
default_value: {}
hide_table_of_contents: true
---

<Tabs
  defaultValue="models"
  values={[
    { label: 'Models', value: 'models', },
    { label: 'Sources', value: 'sources', },
    { label: 'Seeds', value: 'seeds', },
    { label: 'Snapshots', value: 'snapshots', },
    { label: 'Tests', value: 'tests', },
    { label: 'Analyses', value: 'analyses', },
    { label: 'Macros', value: 'macros', },
    { label: 'Exposures', value: 'exposures', },
    { label: 'Semantic Models', value: 'semantic models', },
    { label: 'Metrics', value: 'metrics', },
    { label: 'Saved queries', value: 'saved queries', },
  ]
}>
<TabItem value="models">

<File name='models/schema.yml'>

```yml
version: 2

models:
  - name: model_name
    config:
      meta: {<dictionary>}

    columns:
      - name: column_name
        meta: {<dictionary>}

```

</File>

The `meta` config can also be defined:
- under the `models` config block in `dbt_project.yml`
- in a `config()` Jinja macro within a model's SQL file

See [configs and properties](/reference/configs-and-properties) for details.

</TabItem>

<TabItem value="sources">

<File name='models/schema.yml'>

```yml
version: 2

sources:
  - name: model_name
    config:
      meta: {<dictionary>}

    tables:
      - name: table_name
        config:
          meta: {<dictionary>}

        columns:
          - name: column_name
            meta: {<dictionary>}

```

</File>

</TabItem>

<TabItem value="seeds">

<File name='seeds/schema.yml'>

```yml
version: 2

seeds:
  - name: seed_name
    config:
      meta: {<dictionary>}

    columns:
      - name: column_name
        meta: {<dictionary>}

```

</File>

The `meta` config can also be defined under the `seeds` config block in `dbt_project.yml`. See [configs and properties](/reference/configs-and-properties) for details.

</TabItem>

<TabItem value="snapshots">

<File name='snapshots/schema.yml'>

```yml
version: 2

snapshots:
  - name: snapshot_name
    config:
      meta: {<dictionary>}

    columns:
      - name: column_name
        meta: {<dictionary>}

```

</File>

The `meta` config can also be defined:
- under the `snapshots` config block in `dbt_project.yml`
- in a `config()` Jinja macro within a snapshot's SQL block

See [configs and properties](/reference/configs-and-properties) for details.

</TabItem>

<TabItem value="tests">

You can't add YAML `meta` configs for [generic tests](/docs/build/data-tests#generic-data-tests). However, you can add `meta` properties to [singular tests](/docs/build/data-tests#singular-data-tests) using `config()` at the top of the test file. 

</TabItem>

<TabItem value="analyses">

The `meta` config is not currently supported for analyses.

</TabItem>

<TabItem value="macros">

<File name='macros/schema.yml'>

```yml
version: 2

macros:
  - name: macro_name
    meta: {<dictionary>}

    arguments:
      - name: argument_name

```

</File>

</TabItem>

<TabItem value="exposures">

<File name='models/exposures.yml'>

```yml
version: 2

exposures:
  - name: exposure_name
    meta: {<dictionary>}

```

</File>

</TabItem>

<TabItem value="semantic models">

<File name='models/semantic_models.yml'>

```yml
semantic_models:
  - name: semantic_model_name
    config:
      meta: {<dictionary>}

```

</File>

The `meta` config can also be defined under the `semantic-models` config block in `dbt_project.yml`. See [configs and properties](/reference/configs-and-properties) for details.

</TabItem>

<TabItem value="metrics">

<VersionBlock lastVersion="1.7">

<File name='models/metrics.yml'>

```yml
metrics:
  - name: number_of_people
    label: "Number of people"
    description: Total count of people
    type: simple
    type_params:
      measure: people
    meta:
      my_meta_direct: 'direct'
```

</File>
</VersionBlock>

<VersionBlock firstVersion="1.8"> 
<File name='models/metrics.yml'>

```yml
metrics:
  - name: number_of_people
    label: "Number of people"
    description: Total count of people
    type: simple
    type_params:
      measure: people
    config:
      meta:
        my_meta_config: 'config_value'
```

</File>
</VersionBlock>

</TabItem>

<TabItem value="saved queries">

<File name='models/semantic_models.yml'>

```yml
saved_queries:
  - name: saved_query_name
    config:
      meta: {<dictionary>}
```

</File>

</TabItem>

</Tabs>

## Definition
The `meta` field can be used to set metadata for a resource. This metadata is compiled into the `manifest.json` file generated by dbt, and is viewable in the auto-generated documentation.

Depending on the resource you're configuring, `meta` may be available within the `config` property, and/or as a top-level key. (For backwards compatibility, `meta` is often (but not always) supported as a top-level key, though without the capabilities of config inheritance.)


## Examples
### Designate a model owner
Additionally, indicate the maturity of a model using a `model_maturity:` key.

<File name='models/schema.yml'>

```yml
version: 2

models:
  - name: users
    meta:
      owner: "@alice"
      model_maturity: in dev

```

</File>


### Designate a source column as containing PII

<File name='models/schema.yml'>

```yml
version: 2

sources:
  - name: salesforce

    tables:
      - name: account
        meta:
          contains_pii: true
        columns:
          - name: email
            meta:
              contains_pii: true

```

</File>

### Configure one meta attribute for all seeds

<File name='dbt_project.yml'>

```yml
seeds:
  +meta:
    favorite_color: red
```

</File>

### Override one meta attribute for a single model

<File name='models/my_model.sql'>

```sql
{{ config(meta = {
    'single_key': 'override'
}) }}

select 1 as id
```

</File><br />

### Assign owner and favorite_color in the dbt_project.yml as a config property

<File name='dbt_project.yml'>

```yml
models:
  jaffle_shop:
    +meta:
      owner: "@alice"
      favorite_color: red
```

</File>

