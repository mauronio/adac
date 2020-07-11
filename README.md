# adac
Application Design As Code (ADAC) is a code generation framework starting from a high-level, YAML syntax, functional description of your application. Language-specific code generation is orchestrated and implemented by separate modules, which can be added as 3rd party pluggable providers.

## Principles
# All data is declared
* You declare evey single piece of data relevant to functionality. 
* For each peace of data, you have to declare functional description, persistency requirement, access restrictions, and other attributes which also are relevant to application functionality.
# All operations and sets of operations on data are declared as transactions or scenarios
# Transactions
* Transactions are operations which depend on other transaction calls, or are implemented by the specific generation-provider implementation
* A transaction can be described as a structured (parseable), high-level algorythm of transaction calls
# Scenarios
* A Scenario is a collection of *possible* but not *mandatory* transaction calls or other scenario references
* Scenarios can be seen as GUI menu options, or webservice endpoints in a service catalog 
* Transactions and Scenarios can have *pre* and *post* conditions which, in turn, are transaction calls themselves
# Transactions and scenarios must declare all data that is being used
* Any transaction or scenario has to declare which data it needs.
* Ahy referenced piece of data must have been declared in the global data section

