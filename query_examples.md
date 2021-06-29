Get last height for a specific patient + sex + DOB

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
