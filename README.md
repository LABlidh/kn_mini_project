# Fact-checking engine using SPARQL in Python

## Goal
Build a fact-checking engine which returns a veracity value between 0 (fact is false) and +1 (fact is true) for a given fact with respect to a knowledge graph.<br> 
Apply approaches to real data.<br>
Make use of Semantic Web technologies for a challenging problem.<br>
The veracity value can be any value in the range [0, 1] in case a system is unsure whether a fact is really true or not.<br>
Please do not wait for a lecture that covers this particular task. <br>
The lecture will give you several tools but you need to combine them to create a fact-checking algorithm.

## Data
### Reference knowledge graph
Available as dump file (data\reference-kg.nt)<br>
Available as SPARQL endpoint (https://fokgsw.data.dice-research.org/sparql) (the graph has the IRI https://dice-research.org/students/teaching/fokgsw)<br>

### Training data 
data\fokg-sw-train-2024.nt<br>
RDF statements (we used reification)<br>
The statements have a veracity value assigned (0 or 1).<br>

### Test data 
data\fokg-sw-test-2024.nt<br>
comprise RDF statements (we used reification)<br>

### Class hierarchy 
data\classHierarchy.nt<br>

## In- and Output File of the System
### Input File Format
Here I am unsure, is it like for Example the training data?
I assume it: 
File ending .nt<br>
One line for each fact<br>
Line format: `<Fact-URI> <prop-URI> "value"^^type .`<br>

### Output (Result) File Format
File ending .ttl (e.g., result.ttl)<br>
One line for each of the facts in the input file<br>
Line format: `<Fact-URI> <prop-URI> "value"^^type .`<br>
| **Field**    | **Description**                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------|
| `<Fact-URI>` | URI of the rdf:Statement (`<http://dice-research.org/data/fb15k-237.ttl#0>`, `<http://swc2017.aksw.org/task2/dataset/3892429>`) |
| `<prop-URI>` | always `<http://swc2017.aksw.org/hasTruthValue>`                                                     |
| `value`      | result of the fact checking algorithm (datatype: double)                                             |
| `type`       | always `<http://www.w3.org/2001/XMLSchema#double>` (Type of the value)                               |

#### Example
`<http://swc2017.aksw.org/task2/dataset/3892429><http://swc2017.aksw.org/hasTruthValue>"0.8901"^^<http://www.w3.org/2001/XMLSchema#double> .`

### Example for In- and Output
Input line: <br>
`<http://dice-research.org/data/fb15k-237.ttl#0> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/1999/02/22-rdf-syntax-ns#Statement> .`<br>
`<http://dice-research.org/data/fb15k-237.ttl#0> <http://www.w3.org/1999/02/22-rdf-syntax-ns#subject> <http://rdf.freebase.com/ns/m.0bmssv> .`<br>
`<http://dice-research.org/data/fb15k-237.ttl#0> <http://www.w3.org/1999/02/22-rdf-syntax-ns#predicate> <http://rdf.freebase.com/ns/film.film.featured_film_locations> .`<br>
`<http://dice-research.org/data/fb15k-237.ttl#0> <http://www.w3.org/1999/02/22-rdf-syntax-ns#object> <http://rdf.freebase.com/ns/m.080h2> .`<br>
`<http://dice-research.org/data/fb15k-237.ttl#0> <http://swc2017.aksw.org/hasTruthValue> "1.0"^^<http://www.w3.org/2001/XMLSchema#double> .`<br>
Output line: `<http://dice-research.org/data/fb15k-237.ttl#0> <http://swc2017.aksw.org/hasTruthValue>"0.8901"^^<http://www.w3.org/2001/XMLSchema#double> .`<br>

## Guid 
1. Install Python (https://www.python.org/).
2. Install libary SPARQLWrapper for querying the SPARQL endpoint (pip install rdflib SPARQLWrapper).