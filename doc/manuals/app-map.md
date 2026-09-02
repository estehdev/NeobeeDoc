# AppMap - НРН референце

У наставку су објашњења за колоне у табели es_app_map, за потребе мапирања локалних и екстерних ресурса 
и начина коришћења у апликацијама.

### Колоне:

| назив | тип |
| --- | --- |
| [map_type](#map_type) | VARCHAR(256) |
| [map_subtype](#map_subtype) | VARCHAR(256) |
| [map_subtype_code](#map_subtype_code) | VARCHAR(256) |
| [resolve_model](#resolve_model) | SMALLINT |
| [map_reference_nrn](#map_reference_nrn) | VARCHAR(1024) |



## map_type
Садржи енумерацију доступних типова ресурса за мапирање (нпр., es_process_project, es_process_issue_type, итд.).
Код новијих типова мапирања вредност колоне ће бити *data_def* (es_process_file_template), а старији (*legacy*) типови користе специјалну нотацију (*file_template*), која ће постепено бити избацивана из употребе.

## map_subtype
Садржи допунску информацију о ентитету на који се мапирање односи. На примеру ентитета *ES_ENDPOINT*, ова колона може садржати тип удаљене тачке или интерфејс удаљене тачке који имплементира. (*endpoint_type* ili *endpoint_interface*).

## map_subtype_code
Садржи конкретан идентификатор информације из колоне map_subtype. На примеру ентитета *ES_ENDPOINT*, где у *map_subtype* колони стоји *endpoint_type*, у овој колони би стајала шифра типа удаљене тачке.

**Примери**
| map_type | map_subtype | map_subtype_code | resolve_model | map_reference_nrn | map_reference_to |
| --- | --- | --- | ---: | --- | ---: |
| es_endpoint | **endpoint_type** | **neobee.wordpress** | 4 | nrn:system:es_endpoint:123 | 123 |
| es_endpoint | **endpoint_interface** | **neobee.file** | 4 | nrn:system:es_endpoint:456 | 456 |



## resolve_model
Описује начин учитавања ресурса на који се мапирање односи.
Дозвољене вредности ове колоне су бројеви 1, 2, 3 и 4.

| resolve_model | опис |
| ---: | --- |
| 1 | Локални ресурс из текуће апликације |
| 2 | Локални ресурс из друге апликације на истом систему |
| 3 | Екстерни ресурс - налази се на удаљеном систему |
| 4 | Системски ресурс - налази се на истом систему, али нема app_instance_id |

Системским ресурсом се сматрају ентитети који не подржавају апликативни модел уопште (немају *app_instance_id* колону) и ентитети који подржавају апликативни модел, али немају у датом тренутку постављен *app_instance_id*.

У колону map_type се уписује назив *data_def*-а на који мапирање указује, што би у овом случају било "**es_endpoint**".
Колона map_subtype означава варијанту подтипа, која код удаљене тачке може бити endpoint_type или endpoint_interface.
У случају када је map_subtype попуњен, колона map_subtype_code садржи шифру конкретног подтипа, која може да се користи како би се дати подтип пронашао у бази.
Будући да табела es_endpoint нема везу према апликацији (*app_instance_id*), resolve_model мора да има вредност "**4**", што значи да је у питању системски ресурс.

| map_type | map_subtype | map_subtype_code | resolve_model | map_reference_nrn | map_reference_to |
| --- | --- | --- | ---: | --- | ---: |
| es_endpoint | endpoint_type | neobee.wordpress | 4 | nrn:system:es_endpoint:123 | 123 |
| es_endpoint | endpoint_interface | neobee.file | 4 | nrn:system:es_endpoint:456 | 456 |
| es_process_file_template | *NULL* | *NULL* | 1 | nrn:esteh:esteh:es_process_file_template:333 | 333 |
| es_process_file_template | *NULL* | *NULL* | 3 | nrn:esteh:esteh:es_process_file_template:444 | *NULL* |
| es_process_issue_type | *NULL* | *NULL* | 2 | nrn:neobee:neobee:es_process_issue_type:444 | 444 |

## map_reference_nrn
Садржи НРН референцу према ресурсу, која се снима увек, без обзира на вредност из *resolve_model* колоне.

Примена овог модела се односи само на параметре пост функције чији је тип *APP_MAP*, што је нови тип параметра и мора да се детектује током извршавања функције, тако што ће се учитати дефиниција удаљене тачке из пост функције.
Вредност овог типа параметра ће бити НРН од *es_app_map* записа.

**Пример вредности једног параметра из пост функције:**
```json
{
  "ext_code": "appmap_parametar_u_post_funkciji",
  "value": "nrn:neobee:neobee:es_app_map:123"
}
```

Потребно је учитати es_app_map запис по датом НРН-у.

```sql
select * from es_app_map where nrn = 'nrn:neobee:neobee:es_app_map:123';
```

У том запису постоји колона *map_reference_nrn*, која садржи НРН референцу према конкретном ресурсу. 
У колони *map_type* стоји тип податка на који се референца односи. 
Код нових типова ће то бити баш њихов *data_def*, али је најбоље користити помоћну методу *MoProcess::AppMapManager::getDataDefForMapType*. 

Та референца може бити апликативна, екстерна или системска.

Ако је апликативна или екстерна, потребно је пронаћи запис у табели на коју се *map_type* односи, користећи *map_reference_nrn* за претрагу по колони *nrn*.

**Пример апликативни или екстерни:**
| map_type | map_reference_nrn |
| --- | --- |
| es_process_file_template | nrn:neobee:neobee:es_process_file_template_123 |


```sql
select * from es_process_file_template where nrn='nrn:neobee:neobee:es_process_file_template_123';
```

Ако је системска референца, НРН ће имати специјалан префикс "***nrn:system***":, у ком случају је потребно парсирати ту вредност на начин да се дође до ид-а ресурса.



**Пример системски:**
| map_type | map_reference_nrn |
| --- | --- |
| es_endpoint | nrn:system:es_endpoint:66 |


1. nrn:system:es_endpoint:66 - скида се префикс
2. es_endpoint:66 - узима се табела es_endpoint и у њој се тражи запис са ид-ем 66, или се табела узима из map_type колоне, као у претходном примеру (getDataDefForMapType)
```sql
select * from es_endpoint where id = 66;
```

Вредност ресурса која се добије неким од ова два пута је оно што треба проследити даљем извршавању функције.
