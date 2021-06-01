Shared resources for a medical/physical digital twin project at Linköping University. More info coming later...

##Tools:
* List/browse archetypes (and template examples): https://ckm.openehr.org/ckm/
* Create/edit templates (and if needed also create archetypes):https://tools.openehr.org/designer/
    * ...then export OPT (Operational template) to be used when you...
* **Create GUI/forms and queries**: https://tools.better.care/sandbox/studio/login
* Snomed CT browser: https://browser.ihtsdotools.org/

##Archetype/template links 

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
* Physical exercise... 

