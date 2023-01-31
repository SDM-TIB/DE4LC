## DE4LungCancer

The DE4LungCancer framework is devised as a network of data ecosystems (DEs)[1]; it aligns data and metadata to describe the network and its components. Heterogeneity issues across the different datasets are overcome by various data curation and integration methods. Each DE comprises datasets and programs for accessing, managing, and analyzing their data. Interoperability issues across the datasets of the DEs are solved in a unified schema. Mapping rules between the datasets and the unified schema describe the meaning of the datasets. The metadata layer specifies biomedical vocabularies (e.g., [Unified Medical Language System-UMLS](https://www.nlm.nih.gov/research/umls/index.html) or [Human Phenotype Ontology-HPO](https://hpo.jax.org/app/)). 
 The DE4LungCancer DE is a nested framework that is also composed of three basic DEs: Clinical, Scholarly, and Scientific Open. These basic DEs are described in terms of datasets, metadata, and methods; they enable each basic DE to conduct individual analyses based on locally collected data. On the other hand, the nested DE4LungCancer DE comprises the basic DEs and integrates the data processed by each. As a result, the nested DE4LungCancer DE provides a holistic profile of a lung cancer patient composed of the data process by Clinical, Scholarly, and Scientific Open DEs; these profiles are represented in the DE4LungCancer knowledge graph (KG).

![The DE4LungCancer Data Ecosystem](https://raw.githubusercontent.com/SDM-TIB/DE4LC/main/images/DE4LungCancer.png "The DE4LungCancer Data Ecosystem")


SDM-RDFizer [2], an in-house RML-compliant engine, is utilized to integrate data from the data sources into the KG following the mapping rules. As a result, a KG of 19,602,972 biomedical entities described in terms of 110,788,660 RDF triples is created. Moreover, 3,900,764 links to DBpedia, Wikidata, and UMLS are part of the KG; they are discovered by the tasks of NER and NEL executed by the FnO function included in the mapping rules and by the NLP processes implemented in each DE. The classes -DE4LC:MENTION_IN-, and -DE4LC:HAS_TOPIC- are populated with entities extracted from scientific publications, while -DE4LC:Annotation- comprises the UMLS terms that annotate the entities recognized by the NER implemented on top of the DE4LungCancer datasets.



<p float="left">
  <img src="https://raw.githubusercontent.com/SDM-TIB/DE4LC/main/images/Classes.png" width="300" />
  <img src="https://raw.githubusercontent.com/SDM-TIB/DE4LC/main/images/EntitiesPerClasses.png" width="400" /> 
</p>

## Data Quality and Ethics in the DE4LungCancer Data Ecosystem



## The DE4LungCancer Assessment

### User Acceptance

An initial version of the aforementioned dashboard [8] has been provided to a group of relevant stakeholders to assess its quality and characteristics. Specifically, 44 evaluators have participated in dedicated training and evaluation sessions, running different scenarios, testing the dashboard functionalities, and querying to retrieve data and information of interest. They were then given a questionnaire, asking them to input general profile information and their motivation for utilizing the dashboard The evaluators justified the use of the system and data based on the following reasons: 

- to analyze the characteristics of special populations for queries related to survival curve analysis;  
- to learn how to use the platform and the various functionalities as a knowledge tool about lung cancer; and
- to identify some interesting publications and drug interactions
 
![The initial question of the evaluation questionnaire, in order to identify the stakeholders' groups that participated in the training and evaluation sessions](https://raw.githubusercontent.com/SDM-TIB/DE4LC/main/images/Evaluator_groups.png "The initial question of the evaluation questionnaire, in order to identify the stakeholders' groups that participated in the training and evaluation sessions.")


Finally, the evaluators were asked to rate their overall experience with the dashboard and report any issues found or propose features that they considered missing. The results indicated a positive acceptance by most stakeholders, indicating some features and improvements that could be done for the dashboard to be easily employed in different regions and by various end-users.

![A general rating from the end-users, evaluating their overall experience with the dashboard](https://raw.githubusercontent.com/SDM-TIB/DE4LC/main/images/Platform_evaluation.png "A general rating from the end-users, evaluating their overall experience with the dashboard.")

**References**

[1] S. Geisler, M. Vidal, C. Cappiello, B. F. Lóscio, A. Gal, M. Jarke, M. Lenzerini, P. Missier, B. Otto, E. Paja, B. Pernici, and J. Rehof. Knowledge-driven data ecosystems toward data transparency. ACM J. Data Inf. Qual., 14(1):3:1–3:12, 2022.

[2] E. Iglesias, S. Jozashoori, D. Chaves-Fraga, D. Collarana, and M.-E. Vidal. Sdm-rdfizer: An rml interpreter for the efficient creation of rdf knowledge graphs. In ACM International Conference on Information & Knowledge Management, 2020.

[8] A. Krithara, F. Aisopos, V. Rentoumi, A. Nentidis, K. Bougatiotis, M.-E. Vidal, E. Menasalvas, A. Rodriguez-Gonzalez, E. Samaras, P. Garrard, et al. iasis: Towards heterogeneous big data analysis for personalized medicine. In 2019 IEEE 32nd International Symposium on Computer-Based Medical Systems (CBMS), pages 106–111. IEEE, 2019.



## Authors

Fotis Aisopos, Samaneh Jozashoori, Emetis Niazmand, Disha Purohit, Ariam Rivas, Ahmad Sakor, Enrique Iglesias, Dimitrios Vogiatzis, Ernestina Menasalvas, Alejandro Rodriguez Gonzalez, Guillermo Vigueras, Daniel Gomez-Bravo, Maria Torrente, Roberto Hernández López, Mariano Provencio Pulla, Athanasios Dalianis, Anna Triantafillou, Georgios Paliouras and Maria-Esther Vidal

