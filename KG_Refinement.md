Paper notes [2018/8/6]
[Knowledge Graph Refinement:A Survey of Approaches and Evaluation Methods](http://www.semantic-web-journal.net/system/files/swj1167.pdf)

Construction: use a set of operations on one or more sources to create a KG
Refinement: infer and add missing knowledge/ identify erroneous pieces of info

#### Knowledge graphs in the semantic web

semantic web:graph-based knowledge representation
RDF standards (entities, relations, entities)
organised by a schema/ontology

Linked data: interlink datasets in the semantic web

Knowledge graph: Google 2012
also refer to semantic web knoweldge bases (DBpedia/ YAGO)
more broader, any graph-based representation of some knowledge

##### overview of existing knowledge graph
* Freebase 
* Wikidata
* DBpedia: extracted from Wikipedia
* YAGO: extracted from DBpedia
* NELL: unstructured data
* Google's knowledge graph (semi-structured, structured)
* Google's knowledge vault (extracts from text documents, HTML tables, and structured annotations on the Web), using Freebase. A confident vaule for each fact is computed
* Yahoo!'s Knowledge graph
* Microsoft's Satori
* Facebook's Entities Graph

##### Categorization of Evaluation Methods
* Partial Gold Standard: a subset of graph entities or relations are selected and labeled manually. (or external KGs) => high quality, but costly and small. 
    ps. exploiting other KGs based on KG interlinks (but errors from the target KG or from the linkage between two)
    usually measured by recall, precision, F-measure, ROC-AUC
* KG as Silver Standard: use the given KG itself as a test dataset (not perfect but reasonable quality). Usually applied to measure the performance of KG completion approaches (how well relations in a knowledge graph can replicated by a KG completion method); not suitable for error detection. => underrate the evaluted approach (correctly predicts the existance of an axiom missing in KG, count as a false positive and thus lower precision)
* Retrospective evaluation: human judges => carries out only on samples of the results, allow a very detailed analysis

##### Approaches for Completion of KGs
Goal: increase the coverage of a KG
###### Internal Method
(1) Complete Type assertions: predicting a type/class for an entity given some characteristics of the entity  => classification
* features could be relations (link-based classification problems) e.g. an entity which has a director relation is likely to be a Moive
* probablisitic method (conditional prob) e.g. the prob of a node being of Actor is high if there are ingoing edges of Cast
* SVMs: type entites
* matrix factorization: [Factorizing YAGO: scalable machine learning for linked data](https://dl.acm.org/citation.cfm?id=2187874)
* hierarchical classification problem: **no applications!**
* association rule mining: analyzes co-occurence of items: predict missing info
* topic modelling: entities in a KG are represented as documents: using [Latent Dirichlet Allocation (LDA)](http://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf) to find topics

(2) Predict relations: 
* classification: tensor neural network
* with schema knowledge
* association rule mining
* embedding into a lower dimensional space

###### External methods
use sources of knowledge (e.g. text corpora/ other KGs, which are not part of the KG)
(1) Complete type assertions
* KNN: use Wikipedia link graph to predict types in a KG/ use types of entities in different DBpedia language editions to predict missing types
* use abstracts in DBpedia to extract definitionary clauses (Hearst patterns)
(2) Predict relations
* Distant supervision: use large text corpora. Entities are linked to text corpus (name entity recognition), then seek for text patterns
