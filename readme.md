# Integrating a Digital Twins with openEHR based systems

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

The "Example setup and settings" in https://github.com/modellbibliotek/klinfys-register can be used for testing in this project too.

## Archetype/template links 

#### Prioritized in the Blood glucose predicting digital twin model
* Blood glucose & HbA1c are based on the archetype combination pattern discussed at https://discourse.openehr.org/t/shared-blood-glucose-hba1c-templates/1561/2
    * Local templates of type OBSERVATION to be included in larger template of type COMPOSITION: https://github.com/modellbibliotek/digitaltwin/blob/master/local/Glucose%20test%20result%20example.t.json and https://github.com/modellbibliotek/digitaltwin/blob/master/local/HbA1c%20test%20result.t.json
* Nutrition/meals (e.g. reported from apps like MyFitnesspal etc) - start, length/end, Carbohydrates, Protein (later also Fat)
   *  The [Nutrition intake](https://ckm.openehr.org/ckm/archetypes/1013.1.3564) (OBSERVATION) archetype handles events like Meals/Snacks and can aslo be used to record a cumulative total over a time period (e.g. per day or week). Details for each event is recorded using:
      * the [Dietary nutrients](https://ckm.openehr.org/ckm/archetypes/1013.1.2745) (CLUSTER) archetype recording total fat, protein, carbohydrates etc and can be further detailed using...
          *  ...[Macronutrients](https://ckm.openehr.org/ckm/archetypes/1013.1.2743) and...
          *  ...[Micronutrients](https://ckm.openehr.org/ckm/archetypes/1013.1.2744) archetypes
    *  Alternatively, instead of [Nutrition intake] a set of [Food item](https://ckm.openehr.org/ckm/archetypes/1013.1.2884) (OBSERVATION) entries could be used for recording nutrition. Those items could include detalis via the same above described CLUSTER archetypes (Dietary nutrients, Macronutrients, Micronutrients)
* Height
   * [Height/Length](https://ckm.openehr.org/ckm/archetypes/1013.1.3210)
* Weight
   * [Body weight](https://ckm.openehr.org/ckm/archetypes/1013.1.2960) 
* Gender & Age are in the EHRscape test environment modelled in the EHR status object and already set for each test patient, see AQL-query and example list at https://github.com/modellbibliotek/klinfys-register that is using the same sfmi test domain
* Diagnosis (to know if the person is diagnosed with diabetes)
   * [Problem/Diagnosis](https://ckm.openehr.org/ckm/archetypes/1013.1.169)

#### Later (not currently prioritized) in the Blood glucose twin model
* Physical exercise
* ... 

#### COMPOSITION archetypes ("wrappers" needed in order to be able to store data in openEHR)
* [Self Monitoring](https://ckm.openehr.org/ckm/archetypes/1013.1.2430): 
   * Used in one template (Digital_Twin_Self_Monitoring) used for frequently recurring reports above, like Blood glucose, Nutrition/meals and Body weight as described above
* [Encounter](https://ckm.openehr.org/ckm/archetypes/1013.1.120):
   * Used in another template (Digital_Twin_Base_Data) for reporting Basics that change less frequently. like height and diagnosis

## Queries (AQL)

See separate file https://github.com/modellbibliotek/digitaltwin/blob/master/query_examples.md

