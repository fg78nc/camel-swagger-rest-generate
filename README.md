# camel-swagger-rest-generate

This project is created to validate correctness of the [camel-restdsl-swagger-plugin](https://github.com/apache/camel/blob/master/tooling/maven/camel-restdsl-swagger-plugin/src/main/docs/camel-restdsl-swagger-plugin.adoc
).


Project contains two Swagger v2.0 specification documents in the folder
`src/main/resources`
 
 1.`src/main/resources/swagger.json` - Swagger v2.0 specification document with "troublesome" `enum` elements, 
 which cause `camel-restdsl-swagger-plugin` to fail XML blueprint file generation.
 
 2.`src/main/resources/swagger-xml.json` - Swagger v2.0 specification document without "troublesome" `enum` elements,
  which cause `camel-restdsl-swagger-plugin` to fail XML blueprint file generation.
  
 
### To validate error scenario:
  1. In the `pom.xml` modify configuration of the plugin by changing reference to Swagger specification file: 
  from `swagger-xml.json` to `swagger.json` (as in example below)
      `<specificationUri>src/main/resources/swagger.json</specificationUri>`
  2. Execute from the command line:
    `mvn camel-restdsl-swagger:generate-xml`
     
   The plugin shall fail to executer goal and report:
   
`   Unable to generate REST DSL Swagger sources from specification: src/main/resources/swagger.json: 
    java.lang.NoSuchMethodException: 
        org.apache.camel.model.rest.RestOperationParamDefinition.allowableValues(java.lang.String)
`   


### To validate happy path scenario:
  1. In the `pom.xml` modify configuration of the plugin by changing reference to Swagger specification file: 
  from `swagger.json` to `swagger-xml.json` (as in example below)
      `<specificationUri>src/main/resources/swagger-xml.json</specificationUri>`
  2. Execute from the command line:
    `mvn camel-restdsl-swagger:generate-xml`
   
  The plugin shall report successful execution of goal and `my-blueprint.xml` file shall
  be created at project's `src/main/java` folder
  
  
 
  
  
  
  