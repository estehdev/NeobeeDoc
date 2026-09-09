# AppMap - NRN references

Below are explanations of the columns in the *es_app_map* table, used for mapping local and external resources
and how they are used in applications.

### Columns:

| name | type |
| :--- | :--- |
| [map_type](#map_type) | VARCHAR(256) |
| [map_subtype](#map_subtype) | VARCHAR(256) |
| [map_subtype_code](#map_subtype_code) | VARCHAR(256) |
| [resolve_model](#resolve_model) | SMALLINT |
| [map_reference_nrn](#map_reference_nrn) | VARCHAR(1024) |



## map_type
Contains an enumeration of the available resource types for mapping (e.g., es_process_project, es_process_issue_type, etc.).
For newer mapping types the column value will be the *data_def* (es_process_file_template), while older (*legacy*) types use a special notation (*file_template*), which will gradually be phased out.

## map_subtype
Contains additional information about the entity the mapping refers to. For example, for the *ES_ENDPOINT* entity, this column may contain the endpoint type or the endpoint interface it implements. (*endpoint_type* or *endpoint_interface*).

## map_subtype_code
Contains the concrete identifier of the information from the map_subtype column. For example, for the *ES_ENDPOINT* entity, where the *map_subtype* column holds *endpoint_type*, this column would hold the code of the endpoint type.

**Examples**
| map_type | map_subtype | map_subtype_code | resolve_model | map_reference_nrn | map_reference_to |
| :--- | :--- | :--- | ---: | :--- | ---: |
| es_endpoint | **endpoint_type** | **neobee.wordpress** | 4 | nrn:system:es_endpoint:123 | 123 |
| es_endpoint | **endpoint_interface** | **neobee.file** | 4 | nrn:system:es_endpoint:456 | 456 |



## resolve_model
Describes how the resource the mapping refers to is loaded.
The allowed values of this column are the numbers 1, 2, 3 and 4.

| resolve_model | description |
| ---: | :--- |
| 1 | Local resource from the current application |
| 2 | Local resource from another application on the same system |
| 3 | External resource - located on a remote system |
| 4 | System resource - located on the same system, but has no app_instance_id |

A system resource is considered to be an entity that does not support the application model at all (has no *app_instance_id* column), as well as an entity that supports the application model but does not have *app_instance_id* set at the given moment.

The map_type column stores the name of the *data_def* the mapping points to, which in this case would be "**es_endpoint**".
The map_subtype column denotes the subtype variant, which for an endpoint can be endpoint_type or endpoint_interface.
When map_subtype is filled in, the map_subtype_code column contains the code of the concrete subtype, which can be used to find that subtype in the database.
Since the es_endpoint table has no link to an application (*app_instance_id*), resolve_model must have the value "**4**", meaning it is a system resource.

| map_type | map_subtype | map_subtype_code | resolve_model | map_reference_nrn | map_reference_to |
| :--- | :--- | :--- | ---: | :--- | ---: |
| es_endpoint | endpoint_type | neobee.wordpress | 4 | nrn:system:es_endpoint:123 | 123 |
| es_endpoint | endpoint_interface | neobee.file | 4 | nrn:system:es_endpoint:456 | 456 |
| es_process_file_template | *NULL* | *NULL* | 1 | nrn:esteh:esteh:es_process_file_template:333 | 333 |
| es_process_file_template | *NULL* | *NULL* | 3 | nrn:esteh:esteh:es_process_file_template:444 | *NULL* |
| es_process_issue_type | *NULL* | *NULL* | 2 | nrn:neobee:neobee:es_process_issue_type:444 | 444 |

## map_reference_nrn
Contains the NRN reference to the resource, which is always saved, regardless of the value in the *resolve_model* column.

This model applies only to post function parameters whose type is *APP_MAP*, which is a new parameter type and must be detected during function execution, by loading the endpoint definition from the post function.
The value of this parameter type will be the NRN of the *es_app_map* record.

**Example value of a single parameter from a post function:**
```json
{
  "ext_code": "appmap_param_in_post_function",
  "value": "nrn:neobee:neobee:es_app_map:123"
}
```

The es_app_map record must be loaded by the given NRN.

```sql
select * from es_app_map where nrn = 'nrn:neobee:neobee:es_app_map:123';
```

That record has a *map_reference_nrn* column, which contains the NRN reference to the concrete resource.
The *map_type* column holds the data type the reference refers to.
For new types this will be exactly their *data_def*, but it is best to use the helper method *MoProcess::AppMapManager::getDataDefForMapType*.

That reference can be application-level, external or system-level.

If it is application-level or external, the record must be found in the table that *map_type* refers to, using *map_reference_nrn* to search by the *nrn* column.

**Application-level or external example:**
| map_type | map_reference_nrn |
| :--- | :--- |
| es_process_file_template | nrn:neobee:neobee:es_process_file_template_123 |


```sql
select * from es_process_file_template where nrn='nrn:neobee:neobee:es_process_file_template_123';
```

If it is a system reference, the NRN will have the special prefix "***nrn:system***":, in which case that value must be parsed in order to obtain the resource id.



**System example:**
| map_type | map_reference_nrn |
| :--- | :--- |
| es_endpoint | nrn:system:es_endpoint:66 |


1. nrn:system:es_endpoint:66 - the prefix is stripped
2. es_endpoint:66 - the es_endpoint table is taken and the record with id 66 is looked up in it, or the table is taken from the map_type column, as in the previous example (getDataDefForMapType)
```sql
select * from es_endpoint where id = 66;
```

The resource value obtained through either of these two paths is what should be passed on to the further execution of the function.
