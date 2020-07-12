# adac
Application Design As Code (ADAC) is a code generation framework starting from a high-level, YAML syntax, functional description of your application. Language-specific code generation is orchestrated and implemented by separate modules, which can be added as 3rd party pluggable providers.

# Main Concepts

## All data is declared
* Think of data as "Client ID", "First Name", "Last Name" or "ZIP Code".
* You declare every single piece of data that is relevant to the application functionalities.
* For each peace of data, you have to declare functional description, persistency requirement, access restrictions, and other attributes which also are relevant to application functionality.
## Operations
* All operations and sets of operations on data are declared as *transactions* or *scenarios*.
## Transactions
* A Transaction is any operation on data which can be successful or not whether it be a simple query (where we successfully fetched the required data) or if we execute a complex, orchestrated set of lower-level transactions. 
* Transactions can either depend on other transaction calls, or are implemented by the specific generation-provider implementation.
* A transaction can be described as a structured (parseable), high-level algorythm of transaction calls.
## Scenarios
* A scenario always has successful outcome.
* A Scenario is a collection of *possible* but not *mandatory* transaction calls or other scenario references.
* Scenarios can be seen as GUI menu options, or webservice endpoints in a service catalog .
* Scenarios can have *pre* and *post* conditions which, in turn, are transaction calls themselves. For example, ensuring that the user is authenticated can be a *pre* consition boolean transaction to a secured scenario. And that transaction implementation can imply using an federated authentication (a social network provider, for example) is user is not already aunthenticated. 
## Transactions and scenarios must declare all data that is being used
* Any transaction or scenario has to declare which data it needs.
* Ahy referenced piece of data must have been declared in the global data section.
## Application
* An application is the specific declaration of data, transactions and scenarios and other artifacts that define an application functionality. It is defined in YAML syntax. 
## Complexity Delegation
* For code generation, and code generation orchestration, any extra complexity derived from language, framework or technology, is delegated to code generation providers.
* Code generation orchestration providers are called builder providers, which implement build services. The default build provider will be the default-python-builder, which orchestrate the code generations based on the YAML application declaration. 
* Code generation orchestrators must be given the code generation providers that they have to orchestrate. We can define code generation providers for DJango, AngularJS, Java SpringBoot, Fn functions, Python Flask microservices or any other language/framework of our interest. 
# Application specification file
The application specification is described in the *application.yaml* file, which is the main input for all orchestrators and code generators.
It includes the following sections:
## Data
Data is organized as *attributes* and *entities*. Entities are sets of *attributes*. Entities and attributes have functional descriptions.

The only allowed metadata is declared as *tags*. A tag is a specific functional aspect that may or may not be taken into consideration when generating code. Examples of functional tags are *persistent* (for entities), *non-persistent* (for attributes we dont need to be persistent even though the enclosing entity has to persist), or *indentifier* (for attributes that identify the enclosing entity).  

Any language/framework specific tag that may make sense to a specific code generation provider, must be declared in a specific application mapper file for that generation provider.
