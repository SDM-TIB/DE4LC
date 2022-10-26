Appendix A. Queries to Explore RML Mapping Rules of DE4LungCancer KG

Query 1: SPARQL Query to Retrieve RML Mapping Rules defining the class LCPatient

PREFIX rr:  <http://www.w3.org/ns/r2rml#>
PREFIX rml: <http://semweb.mmlab.be/ns/rml#>
PREFIX lc:  <http://bigmedilytics.eu/vocab/>

SELECT DISTINCT ?mappingRule ?logicalSource ?predicate ?sourceAttribute
WHERE {
?mappingRule rml:logicalSource ?ls.
?ls          rml:source        ?logicalSource.
?mappingRule rr:subjectMap     ?subject.
?subject     rr:class          lc:LCPatient.
OPTIONAL {   ?mappingRule rr:predicateObjectMap ?pObjectMap .
             ?pObjectMap  rr:predicate          ?predicate .
             ?pObjectMap  rr:objectMap          ?objectMap .
             ?objectMap   ?mode                 ?sourceAttribute}} 
--------------------------------------------------------------------------------------------------
Query 2: SPARQL Query to Retrieve FnO Functions Called in Mapping Rules

PREFIX rr:   <http://www.w3.org/ns/r2rml#>
PREFIX rml:  <http://semweb.mmlab.be/ns/rml#>
PREFIX fnml: <http://semweb.mmlab.be/ns/fnml#>
SELECT DISTINCT ?functionCall ?argument ?action  ?argumentValue
WHERE {
?functionCall fnml:functionValue    ?fv.
?fv           rr:predicateObjectMap ?pom .
?pom          rr:predicate          ?argument .
?pom          rr:objectMap          ?om .                  
?om           ?action               ?argumentValue   
FILTER (?action in (rml:reference, rr:constant))}
==================================================================================================
Appendix B. Queries to Explore the Open DE4LungCancer KG

Query 3: DDIs identified in each of the Lung Cancer treatments

PREFIX de4lc: <http://research.tib.eu/DE4LC/vocab/>
PREFIX de4lcE: <http://research.tib.eu/DE4LC/entity/>
SELECT DISTINCT * 
WHERE {
?treatment  de4lc:hasDDIs_DeductiveSystem  ?ddiDS .
?treatment  de4lc:hasTreatmentDrug         ?drug .
?treatment  de4lc:hasDDIs_DrugBank         ?ddiDB .
?treatment  de4lc:hasDDIs_Literature       ?ddiL .
BIND(de4lcE:0_Treatment as ?treatment)    }
--------------------------------------------------------------------------------------------------
Query 4: Comparison of DDIs Extracted From DrugBank versus the Deduced DDIs

PREFIX de4lc: <http://research.tib.eu/DE4LC/vocab/>
PREFIX de4lcE: <http://research.tib.eu/DE4LC/entity/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
SELECT ?treatment ?extensionalDDI ?intensionalDDI 
((xsd:float(?intensionalDDI - ?extensionalDDI)/
xsd:float(?extensionalDDI))*100 as ?percentageGain) 
WHERE {
SELECT ?treatment (COUNT(distinct ?ddiDB) AS ?extensionalDDI) 
(COUNT(distinct ?ddiDS) AS ?intensionalDDI) 
WHERE {
?treatment  de4lc:hasDDIs_DeductiveSystem  ?ddiDS .
?treatment  de4lc:hasDDIs_DrugBank         ?ddiDB .
     } GROUP BY ?treatment 
     } ORDER BY DESC(?percentageGain)
--------------------------------------------------------------------------------------------------
Query 5: Comparison of DDIs Extracted From DrugBank versus the Predicted DDIs Using Literature

PREFIX de4lc: <http://research.tib.eu/DE4LC/vocab/>
PREFIX de4lcE: <http://research.tib.eu/DE4LC/entity/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
SELECT ?treatment ?extensionalDDI ?predictedDDI 
((xsd:float(?predictedDDI - ?extensionalDDI)/
xsd:float(?extensionalDDI))*100 as ?percentagePrediction) 
WHERE {
SELECT ?treatment (COUNT(distinct ?ddiDB) AS ?extensionalDDI)
(COUNT(distinct ?ddiL) AS ?predictedDDI) 
WHERE {?treatment de4lc:hasDDIs_Literature ?ddiL .
       ?treatment de4lc:hasDDIs_DrugBank ?ddiDB .
       } GROUP BY ?treatment } 
       ORDER BY DESC(?percentagePrediction)
--------------------------------------------------------------------------------------------------
Query 6: Comparison of Drugs and DDIs (Extracted from DrugBank) Per Treatment

PREFIX de4lc: <http://research.tib.eu/DE4LC/vocab/>
PREFIX de4lcE: <http://research.tib.eu/DE4LC/entity/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
SELECT ?treatment ?numberOfDrugs ?numDDIs 
((xsd:float(?numDDIs - ?numberOfDrugs)/
xsd:float(?numberOfDrugs))*100 as ?DDIsPerDrugs) 
WHERE {
        SELECT ?treatment (COUNT(distinct ?drug) AS ?numberOfDrugs) 
        (COUNT(distinct ?ddiDB) AS ?numDDIs) 
    WHERE {
    ?treatment  de4lc:hasTreatmentDrug  ?drug .
    ?treatment  de4lc:hasDDIs_DrugBank  ?ddiDB .
          } 
        GROUP BY ?treatment } 
        ORDER BY DESC(?DDIsPerDrugs)
--------------------------------------------------------------------------------------------------
Query 7: Comparison of Drugs and DDIs (Extracted from DrugBank and Deduced using DS) Per Treatment

PREFIX de4lc: <http://research.tib.eu/DE4LC/vocab/>
PREFIX de4lcE: <http://research.tib.eu/DE4LC/entity/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
SELECT ?treatment ?numberOfDrugs ?numDDIs ?numDeducedDDIs 
((xsd:float(?numDDIs - ?numberOfDrugs)/
xsd:float(?numberOfDrugs))*100 as ?DDIsPerDrugs) 
((xsd:float(?numDeducedDDIs ?numberOfDrugs)/
xsd:float(?numberOfDrugs))*100 as ?DeducedDDIsPerDrugs)
WHERE {
        SELECT ?treatment (COUNT(distinct ?drug) AS ?numberOfDrugs) 
        (COUNT(distinct ?ddiDB) AS ?numDDIs) 
        (COUNT(distinct ?ddiDS) AS ?numDeducedDDIs) 
        WHERE {
        ?treatment  de4lc:hasTreatmentDrug         ?drug .
        ?treatment  de4lc:hasDDIs_DrugBank         ?ddiDB .
        ?treatment  de4lc:hasDDIs_DeductiveSystem  ?ddiDS .
               } GROUP BY ?treatment } 
               ORDER BY DESC(?numberOfDrugs)
--------------------------------------------------------------------------------------------------
Query 8: The Top 20 Drugs that are most used in the treatments

PREFIX de4lc: <http://research.tib.eu/DE4LC/vocab/>
PREFIX de4lcE: <http://research.tib.eu/DE4LC/entity/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
SELECT ?drugLabel
(COUNT(distinct ?treatment) AS ?numberOfTreatments) 
WHERE {
        ?treatment   de4lc:hasTreatmentDrug   ?drug .
        ?drug        de4lc:drugLabel          ?drugLabel .
       } 
       GROUP BY ?drugLabel  
       ORDER BY DESC(?numberOfTreatments) 
       LIMIT 20
--------------------------------------------------------------------------------------------------