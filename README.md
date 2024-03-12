# Engineering Knowledge for Autonomous Agents

To use the Ekaa ontology, please include all dependent ontologies (`automation-model, engineering-ontologies, process-model, process-model-tso, requirements-ontology, and system-design-ontology`) while importing to a graph database.

In the `/ekaa/demo` folder there are example engineering descriptions that can be used to test inference queries. Amongst these, the easiest to get started is the sandbox.ttl -- it is a self-contained knowledge graph of demonstrating a simple heating system in a room.

Once the ontologies and instances are loaded in a graph database, SPARQL queries like the following one can be used:
```
prefix eka: <http://w3id.org/unified-engineering/ekaa#>
construct{
    ?intent eka:hasGoal ?goal.
    ?intent eka:utilizes ?process.
    ?intent eka:utilizes ?sys.
}
where { 
    ?intent a eka:Intent.
    ?req a eka:Requirement.
	?req eka:concerns ?con.
    ?sys a eka:System.
    ?sys eka:serves ?con.
    
    ?req eka:hasGoal ?goal.
    ?goal eka:hasDesiredState ?gs.
    ?gs eka:refersToVariable ?var.
    ?process a eka:Process.
    ?process eka:hasMechanism* ?mechanism.
    ?mechanism eka:hasVariable ?var.

}
```