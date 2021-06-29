### Get last height for a specific patient + sex + DOB

```
SELECT s/data[at0001]/events[at0002]/data[at0003]/items[at0004]/value/magnitude AS height,
       e/ehr_id/value as ehrID,
       e/ehr_status/subject/external_ref/id/value AS patient_id,
       e/ehr_status/other_details/items[at0001]/value/value as sex,
       e/ehr_status/other_details/items[at0002]/value/value as date_of_birth,
       s/data[at0001]/events[at0002]/time/value AS measurement_time
FROM EHR e
--CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.encounter.v1] 
CONTAINS OBSERVATION s[openEHR-EHR-OBSERVATION.height.v2]
--WHERE height < 166
WHERE ehrID = 'a3aaa0be-137a-4d8d-a086-1c21e710e77c'
--WHERE patient_id = '1448204'
ORDER BY measurement_time DESCENDING
OFFSET 0 LIMIT 1
```

### All lab values values
```
SELECT j/items[at0024]/value AS analyte_name,
       j/items[at0024]/value/defining_code/code_string AS analyte_code_string,
       j/items[at0001]/value AS Analyte_result
FROM EHR e
CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.self_monitoring.v0] 
CONTAINS CLUSTER j[openEHR-EHR-CLUSTER.laboratory_test_analyte.v1] 
OFFSET 0 LIMIT 10
```

### Glucose (continuous...) values values
```
SELECT j/items[at0024]/value AS analyte_name,
       j/items[at0024]/value/defining_code/code_string AS analyte_code_string,
       j/items[at0001]/value AS Analyte_result
FROM EHR e
CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.self_monitoring.v0] 
CONTAINS CLUSTER j[openEHR-EHR-CLUSTER.laboratory_test_analyte.v1] 
WHERE analyte_code_string = '439926003'
OFFSET 0 LIMIT 10
```
### Glucose (continuous...) values values with time
```
SELECT l/items[at0001]/value/magnitude AS Analyte_result_magnitude,
       l/items[at0001]/value/units AS Analyte_result_unitd,
       l/items[at0024]/value/value AS Analyte_name,
       l/items[at0024]/value/defining_code/code_string AS Analyte_SNOMED_CT_code,
       p/data[at0001]/events[at0002,'Blood glucose']/time/value AS time_value
FROM EHR e
CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.self_monitoring.v0] 
CONTAINS OBSERVATION p[openEHR-EHR-OBSERVATION.laboratory_test_result.v1]
CONTAINS (CLUSTER l[openEHR-EHR-CLUSTER.laboratory_test_analyte.v1] and CLUSTER f[openEHR-EHR-CLUSTER.specimen.v1]) 
WHERE Analyte_SNOMED_CT_code = '439926003'
OFFSET 0 LIMIT 10
```

### REST/https POSTing via API

By posting the query below to https://rest.ehrscape.com/rest/openehr/v1/query/aql (via your own code or a tool like Postman) using basic authentication with the sfmi user and password...

```
{
  "q": "SELECT l/items[at0001]/value/magnitude AS Analyte_result_magnitude,
       l/items[at0001]/value/units AS Analyte_result_unitd,
       l/items[at0024]/value/value AS Analyte_name,
       l/items[at0024]/value/defining_code/code_string AS Analyte_SNOMED_CT_code,
       p/data[at0001]/events[at0002,'Blood glucose']/time/value AS time_value
FROM EHR e
CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.self_monitoring.v0] 
CONTAINS OBSERVATION p[openEHR-EHR-OBSERVATION.laboratory_test_result.v1]
CONTAINS (CLUSTER l[openEHR-EHR-CLUSTER.laboratory_test_analyte.v1] and CLUSTER f[openEHR-EHR-CLUSTER.specimen.v1]) 
WHERE Analyte_SNOMED_CT_code = '439926003'
OFFSET 0 LIMIT 10"
}
```

...you could get something like the following in response ...

```
{
  "meta": {
    "_type": "RESULTSET",
    "_created": "2021-06-29T14:57:43.177Z",
    "_executed_aql": "SELECT l/items[at0001]/value/magnitude AS Analyte_result_magnitude,        l/items[at0001]/value/units AS Analyte_result_unitd,        l/items[at0024]/value/value AS Analyte_name,        l/items[at0024]/value/defining_code/code_string AS Analyte_SNOMED_CT_code,        p/data[at0001]/events[at0002,'Blood glucose']/time/value AS time_value FROM EHR e CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.self_monitoring.v0]  CONTAINS OBSERVATION p[openEHR-EHR-OBSERVATION.laboratory_test_result.v1] CONTAINS (CLUSTER l[openEHR-EHR-CLUSTER.laboratory_test_analyte.v1] and CLUSTER f[openEHR-EHR-CLUSTER.specimen.v1])  WHERE Analyte_SNOMED_CT_code = '439926003' OFFSET 0 LIMIT 10"
  },
  "q": "SELECT l/items[at0001]/value/magnitude AS Analyte_result_magnitude,        l/items[at0001]/value/units AS Analyte_result_unitd,        l/items[at0024]/value/value AS Analyte_name,        l/items[at0024]/value/defining_code/code_string AS Analyte_SNOMED_CT_code,        p/data[at0001]/events[at0002,'Blood glucose']/time/value AS time_value FROM EHR e CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.self_monitoring.v0]  CONTAINS OBSERVATION p[openEHR-EHR-OBSERVATION.laboratory_test_result.v1] CONTAINS (CLUSTER l[openEHR-EHR-CLUSTER.laboratory_test_analyte.v1] and CLUSTER f[openEHR-EHR-CLUSTER.specimen.v1])  WHERE Analyte_SNOMED_CT_code = '439926003' OFFSET 0 LIMIT 10",
  "columns": [
    {
      "name": "Analyte_result_magnitude",
      "path": "/items[at0001]/value/magnitude"
    },
    {
      "name": "Analyte_result_unitd",
      "path": "/items[at0001]/value/units"
    },
    {
      "name": "Analyte_name",
      "path": "/items[at0024]/value/value"
    },
    {
      "name": "Analyte_SNOMED_CT_code",
      "path": "/items[at0024]/value/defining_code/code_string"
    },
    {
      "name": "time_value",
      "path": "/data[at0001]/events[at0002]/time/value"
    }
  ],
  "rows": [
    [
      8,
      "mmol/L",
      "Ambulatory continuous glucose monitoring of interstitial tissue fluid (procedure)",
      "439926003",
      "2021-06-29T16:11:19.774915+02:00"
    ],
    [
      9,
      "mg/dl",
      "Ambulatory continuous glucose monitoring of interstitial tissue fluid (procedure)",
      "439926003",
      "2021-06-29T16:34:15.696727+02:00"
    ]
  ]
}
```

You could also try the same in the https://www.ehrscape.com/api-explorer.html web interface (under `OpenEhr REST API` --> `/query` --> `POST`) provided that you have entered the sfmi user and password in the settings (accesed via button with cog-wheel as in screenshot below)

![image](https://user-images.githubusercontent.com/1034001/123822531-aa923980-d8fc-11eb-9918-8cf239de4d73.png)
