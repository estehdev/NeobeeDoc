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
| [is_export_enabled](#is_export_enabled) | INT |
| [is_edit_enabled](#is_edit_enabled) | INT |


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

## is_export_enabled
Означава особину мапирања која говори да ли се дати ресурс извози са апликацијом.

- Уколико је 1, ресурс се извози и мапирање ће имати референцу према ресурсу (*map_reference_nrn*, *map_reference_to*)
- Уколико је 2 или NULL, референца ресурса из мапирања неће бити присутна у извозу, нити ће се током инсталације узимати у обзир. Вредност NULL се у извоз уписује као 2.

Референца се извози само ако су испуњени сви услови:
- *is_export_enabled* = 1
- ресурс на који мапирање показује има *app_instance_id*
- *resolve_model* није 4 (системски ресурс)
- извоз познаје табелу за дати *map_type* (*MoProcess::ProcessExportManager::getTableNameForMapType*)

Типови за које се референца може извести: *file_template*, *es_process_file_template*, *role*, *process_filter*, *user_group*, *process_custom_table*, *process_priority*, *process_issue_type*, *es_process_issue_type*, *permission_scheme*, *es_process_project*.

За *endpoint_smtp*, *endpoint*, *es_endpoint*, *ai_config* и *content_index* референца се никада не извози, па вредност 1 нема ефекта.

## is_edit_enabled
Означава особину мапирања која говори да ли је могуће мењати мапирање на дестинационом систему. 
Односи се на референцу према ресурсу и на природу мапирања (*map_reference_nrn*, *map_reference_to*, *resolve_model*).

- Уколико је 1, мапирање је могуће мењати на дестинационом систему. Мапирање које је могуће мењати неће бити ажурирано поновном инсталацијом.
- Уколико је 2, мапирање је није могуће мењати на дестинационом систему. Оваква мапирања се аутоматски ажурирају поновном инсталацијом.
- Вредност NULL се у извоз уписује као 1.

На закључаној апликацији *AppMapPicker* не дозвољава промену изабраног мапирања када је *is_export_enabled* = 1, а *is_edit_enabled* различито од 1.

| Комбинације | is_export_enabled=1 | is_export_enabled=2 |
| :--- | :--- | :--- |
| **is_edit_enabled=1** | извози се, може да се мења | не извози се, може да се мења |
| **is_edit_enabled=2** | извози се, не може да се мења | неисправна ситуација |

На развојном систему се виде сва мапирања, без обзира на њихову измењивост, док се на дестинационом систему виде само она која је могуће мењати.

## Подразумеване вредности за is_export_enabled и is_edit_enabled
База нема подразумеване вредности за ове две колоне. Бекенд (*MoProcess::AppMapManager::createAppMapReference*, као и његов порт у MoUser-у) уписује само оно што стигне у захтеву. Ако параметар не постоји, колона остаје NULL.

**Подразумеване вредности одређује искључиво фронтенд.**

Постојећи записи са NULL вредностима ажурирани су скриптом *929.sql*: *is_export_enabled* на 2, *is_edit_enabled* на 1.

### Вредности по начину креирања
| Начин креирања | is_export_enabled / is_edit_enabled |
| :--- | :--- |
| *AppMapPicker*, креирање новог мапирања | по типу, из табеле испод |
| Мапирање апликације (*ApplicationInstanceMapping*, NeobeeAdminTenantFrontend), креирање | по типу, из табеле испод. Примењује се при отварању прозора и при промени типа, док корисник не промени прекидаче. |
| *should_create_app_map* при креирању улоге, приоритета, шаблона фајла, филтера, корисничке групе и прилагођене табеле | 1 / 2. Вредности шаље фронтенд, а бекенд их само преноси (*AppMapManager::createAppMapReferenceForEntity*). |
| Подразумевана шема дозвола при креирању инстанце апликације или пројекта | 1 / NULL. Постојећи изузетак: вредност поставља бекенд. |
| Директан позив *create_app_map_reference* без ових параметара | NULL / NULL |
| Инсталација (увоз) | вредности из извоза |

### Вредности по типу (AppMapPicker и мапирање апликације)
Табела се налази у NeobeeUI-ју, у *src/util/project-management.js* (*AppMapCreateDefaults*, *getAppMapCreateDefaults*). Подразумеване вредности се мењају само ту.

| Група | map_type | is_export_enabled / is_edit_enabled | Разлог |
| :--- | :--- | :--- | :--- |
| Ресурси апликације које корисник може да замени | *permission_scheme*, *process_filter*, *role*, *user_group*, *process_priority*, *file_template*, *es_process_file_template* и сви остали типови без посебне вредности | 1 / 1 | Ресурс се испоручује са апликацијом. Корисник га може заменити својим (нпр. дозволе и групе се разликују по кориснику), а измена се задржава при поновној инсталацији. |
| Структурни ресурси апликације | *process_custom_table*, *process_issue_type*, *es_process_issue_type*, *es_process_project* | 1 / 2 | Логика апликације зависи од њихове тачне структуре. Замена на закључаној апликацији покварила би функције, упите и токове. |
| Ресурси везани за окружење | *endpoint_smtp*, *endpoint*, *es_endpoint*, *ai_config*, *content_index* | 2 / 1 | Референца се ионако не извози. Свако окружење има своје SMTP сервере, креденцијале, AI кључеве и индексе, па мапирање мора бити могуће мењати. |

Ниједан начин креирања не даје комбинацију *is_export_enabled* = 2 и *is_edit_enabled* = 2 (неисправна ситуација из табеле комбинација).