Shared resources for data nosmalisation/standardisation to be used in a medical/physical digital twin project at Linköping University, IMT (Gunnar Cedersund et.al.) + Region Östergötland. See image 
* About the digital twin in English https://www.youtube.com/watch?v=MvWPHM7wWV4
* Longer in Swedish; Part 1: https://www.youtube.com/watch?v=8geMW5lpSs4 Part2: https://www.youtube.com/watch?v=SxtxhjR-lAU 
![image](https://user-images.githubusercontent.com/1034001/120607667-b0594400-c450-11eb-8894-435619974e3d.png)

## Tools:
* List/browse archetypes (and template examples): https://ckm.openehr.org/ckm/
* Create/edit templates (and if needed also create archetypes):https://tools.openehr.org/designer/
    * ...then export OPT (Operational template) to be used when you...
* **Create GUI/forms and queries**: https://tools.better.care/sandbox/studio/login
* Snomed CT browser: https://browser.ihtsdotools.org/

The "Example setup and settings" in https://github.com/modellbibliotek/klinfys-register can be used fpr testing in this project too.

## Archetype/template links 

#### COMPOSITION archetypes ("wrappers" needed in order to be able to store data in openEHR)
* Self reporting: https://github.com/modellbibliotek/digitaltwin/blob/master/local/Digital_Twin_Self_Report_test1.t.json
* Encounter

#### Prioritized in the Blood glucose twin model
* Blood glucose (in plasma)
    * discussion https://discourse.openehr.org/t/shared-blood-glucose-hba1c-templates/1561/2
    * Local templates: https://github.com/modellbibliotek/digitaltwin/blob/master/local/Glucose%20test%20result%20example.t.json and https://github.com/modellbibliotek/digitaltwin/blob/master/local/HbA1c%20test%20result.t.json
* Nutrition/meals (e.g. reported from apps like MyFitnesspal etc) - start, length/end, Carbohydrates, Protein (later also Fat)
* Height
* Weight
* Gender
* Diagnosis (to know if the person is diagnosed with diabetes)

#### Later in the Blood glucose twin model
* Physical exercise
* ... 

