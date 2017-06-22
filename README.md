# simpleSPARQLJS
SimpleSPARQLJS is a very simple sparql library for javascript. It is very lightweight and completely written in JS. Currently it only supports select and ask. 

# Usage
The usage is quite easy and tried to mirror a little bit the JENA API. 

## Create Query
This will just create a query object for itself. It can be queried against different SPARQL enpoints. 
Currently it will not be parsed if the query is correct
``` javascript
var query = createQuery("SELECT * WHERE {?s ?p ?o} LIMIT 10");
```

## Execute Query
Once created, the query can be executed against a sparql endpoint.
``` javascript
query.select("http://dbpedia.org/sparql");
```
or
``` javascript
query.ask("http://dbpedia.org/sparql");
```

## Get Results
Once executed, the results are saved in
``` javascript
var results = query.results;
```
For select (iterate over all results):
``` javascript
results.vars //returns the variable used (in the example "s, p, o")
while(results.hasNext()){ 
  //checks if another row exists.
  results.next(); //incr index to the next row
  for(i=0;i < results.vars.length;i++) {
    //results.getFromIndex(0); 
    results.getFromVarName(results.vars[i]);
  }
}
```
For ask:
``` javascript
results // "true" or "false"
```

### Reset SELECT Row Pointer
if you want to start from the begin of the results you can reset the index pointer
``` javascript
results.reset();
```
