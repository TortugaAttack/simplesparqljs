# simpleSPARQLJS
SimpleSPARQLJS is a very simple sparql library for javascript. It is very lightweight and completely written in JS. Currently it only supports select and ask. 

# Usage
The usage is quite easy and tried to mirror a little bit the JENA API. 

## Create Query
This will just create a query object for itself. It can be queried against different SPARQL enpoints. 
Currently it will not be parsed if the query is correct
```
var query = createQuery("SELECT * WHERE {?s ?p ?o} LIMIT 10");
```

## Execute Query
Once created, the query can be executed against a sparql endpoint.
```
query.select("http://dbpedia.org/sparql");
```
or
```
query.ask("http://dbpedia.org/sparql");
```

## Get Results
Once executed, the results are saved in
```
var results = query.results;
```
For select (iterate over all results):
```
results.vars //returns the variable used (in the example "s, p, o")
while(results.hasNext()){ 
  //checks if another row exists.
  results.next(); //incr index to the next row
  for(var sparqlVar in results.vars){
    //results.getFromIndex(0); 
    results.getFromIndex(sparqlVar);
}
```
For ask:
```
results // "true" or "false"
```
