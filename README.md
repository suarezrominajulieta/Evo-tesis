Que tener instalado:

C:\Users\Usuario>python --version
Python 3.13.5

C:\Users\Usuario>pip --version
pip 25.1.1 from C:\Users\Usuario\AppData\Local\Programs\Python\Python313\Lib\site-packages\pip (python 3.13)

C:\Users\Usuario>npm --version
10.9.2

Tener Docker instalado y corriendo.

Variables de sistema en windows:

En cmd: set JDK_JAVA_OPTIONS=--add-opens java.base/java.util.regex=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED -Djdk.attach.allowAttachSelf=true

o crear una variable de entorno de sistema, "JDK_JAVA_OPTIONS", con el valor: --add-opens java.base/java.util.regex=ALL-UNNAMED --add-opens java.base/java.net=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED -Djdk.attach.allowAttachSelf=true.

--------------------------------------------------

mvn clean install -X -DskipTests

para averiguar el openApí: http://localhost:8080/v3/api-docs

--------------------------------------------------

.XML:

java -jar ./core/target/evomaster.jar  --blackBox true --bbSwaggerUrl file:///C:/Users/Usuario/Documents/GitHub/Evo-tesis/EvoMaster-master/SchemaXml.json --bbTargetUrl http://localhost:8080 --outputFormat JAVA_JUNIT_5 --outputFolder ./evomaster-tests --maxTime 30s --ratePerMinute 60

bien ahora investigar porque el body no se crea

--------------------------------------------------

.Json patch :

java -jar ./core/target/evomaster.jar  --blackBox true --bbSwaggerUrl file:///C:/Users/Usuario/Documents/GitHub/Evo-tesis/EvoMaster-master/SchemaJsonPatch.json --bbTargetUrl http://localhost:8080 --outputFormat JAVA_JUNIT_5 --outputFolder ./evomaster-tests --maxTime 30s --ratePerMinute 60


2025-06-02 19:46:45.141  WARN 19820 --- [nio-8080-exec-9] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotReadableException: JSON parse error: Cannot deserialize value of type `java.util.ArrayList<com.github.fge.jsonpatch.JsonPatchOperation>` from Object value (token `JsonToken.FIELD_NAME`); nested exception is com.fasterxml.jackson.databind.exc.MismatchedInputException: Cannot deserialize value of type `java.util.ArrayList<com.github.fge.jsonpatch.JsonPatchOperation>` from Object value (token `JsonToken.FIELD_NAME`)
 at [Source: (PushbackInputStream); line: 2, column: 21]]
2025-06-02 19:46:45.141 ERROR 19820 --- [nio-8080-exec-9] o.a.c.c.C.[Tomcat].[localhost]           : Exception Processing ErrorPage[errorCode=0, location=/error]
19:46:49.180 [main] WARN  o.e.c.o.service.HttpWsTestCaseWriter - Currently no assertions are generated for response type: text/html;charset=utf-8
19:46:17.488 [main] WARN  o.e.c.s.service.SearchTimeController - The SUT sent a 'Connection: close' HTTP header. This should be avoided, if possible


/**
    * Calls:
    * (400) PATCH:/api/patch
    * Found 1 potential fault of type-code 200
    */
    @Test @Timeout(60)
    public void test_0_patchOnPatchReturnsSchemaInvalidResponse() throws Exception {
        
        // Fault200. Received A Response From API That Is Not Valid According To Its Schema. PATCH:/api/patch -> Response status 400 not defined for path '/api/patch'.
        given().accept("*/*")
                .contentType("application/json-patch+json")
                .body(" { " + 
                    " \"EM_tainted_map\": \"_EM_0_XYZ_\" " + 
                    " } ")
                .patch(baseUrlOfSut + "/api/patch")
                .then()
                .statusCode(400)
                .assertThat()
                .contentType("text/html");
    }

--------------------------------------------------

.MULTIPART/FORM-DATA:

java -jar evomaster.jar  --blackBox true --bbSwaggerUrl file:///C:/Users/Usuario/Documents/GitHub/Evo-tesis/EvoMaster-master/SchemaMulti.json --bbTargetUrl http://localhost:8080 --outputFormat JAVA_JUNIT_5 --outputFolder ./evomaster-tests --maxTime 30s --ratePerMinute 60
  
    /**
    * Calls:
    * (415) POST:/api/multi/upload
    * Found 1 potential fault of type-code 200
    */
    @Test @Timeout(60)
    public void test_0_postOnUploadReturnsSchemaInvalidResponse() throws Exception {
        
        // Fault200. Received A Response From API That Is Not Valid According To Its Schema. POST:/api/multi/upload -> Response status 415 not defined for path '/api/multi/upload'.
        given().accept("*/*")
                .contentType("application/x-www-form-urlencoded")
                .body("file=Gy&description=3NvJ8HEcQDgodH")
                .post(baseUrlOfSut + "/api/multi/upload")
                .then()
                .statusCode(415)
                .assertThat()
                .contentType("text/html");
    }
    /**
    * Calls:
    * (415) POST:/api/multi/upload
    * Found 1 potential fault of type-code 200
    */
    @Test @Timeout(60)
    public void test_0_postOnUploadReturnsSchemaInvalidResponse() throws Exception {
        
        // Fault200. Received A Response From API That Is Not Valid According To Its Schema. POST:/api/multi/upload -> Response status 415 not defined for path '/api/multi/upload'.
        given().accept("*/*")
                .contentType("application/x-www-form-urlencoded")
                .body("")
                .post(baseUrlOfSut + "/api/multi/upload")
                .then()
                .statusCode(415)
                .assertThat()
                .contentType("text/html");
    }

--------------------------------------------------

para correr solo 1 test (no correr todos tests en local, usar CI en GitHub, tarda 2hs):

mvn -pl e2e-tests/spring-rest-openapi-v3 -Dtest=WmAuth0EMTest test

--------------------------------------------------

Deshabilite todos estos tests para correr el local:

Ambos test de AHypermutationAWHTest, de ambos modulos.

WmAuth0EMTest
WmJsonMapEMTest
WmOkHttpEMTest
WmUrlOpenEMTest
WMHttpsTest

BBAuthCookieEMTest.testBlackBoxOutput
BBAuthCookieRedirectEMTest.testBlackBoxOutput
BBAuthEMTest.testBlackBoxOutput
BBAuthTokenEMTest.testBlackBoxOutput
BBChainedLocationEMTest.testBlackBoxOutput
BBCleanUpEMTest.testBlackBoxOutput
BBCoverageQueryEMTest.testBlackBoxOutput
BBDataPoolEMTest.testBlackBoxOutput
BBDefaultEMTest.testBlackBoxOutput
BBExampleObjectEMTest.testBlackBoxOutput
BBExamplesEMTest.testBlackBoxOutput
BBInputsEMTest.testBlackBoxOutput
BBLinksEMTest.testBlackBoxOutput
BBLinksMultiEMTest.testBlackBoxOutput
BBPrimitivesEMTest.testBlackBoxOutput
BBExamplesEMTest.testBlackBoxOutput

--------------------------------------------------

Para correr mi application, ponerla en run desde intellij, en el puerto 8080 por defecto y correr para generar los tests asi:

mvn clean install -X -DskipTests

java -jar core/target/evomaster.jar  --blackBox true --bbSwaggerUrl file:///C:/Users/Usuario/Documents/GitHub/SchemaXml.json --bbTargetUrl http://localhost:8080 --outputFormat JAVA_JUNIT_5 --outputFolder ./evomaster-tests --maxTime 30s --ratePerMinute 60

Correr todos los tests del modulo evomaster-e2e-tests-spring-rest-openapi-v3:

mvn test -pl :evomaster-e2e-tests-spring-rest-openapi-v3

O solo el mio:

mvn test -pl :evomaster-e2e-tests-spring-rest-openapi-v3 -Dtest=XmlEMTest -X

Para correr la de pet store, ver que la este corriendo docker, y ver el puerto donde:

java -jar core/target/evomaster.jar --blackBox true --bbSwaggerUrl file:///C:/Users/Usuario/Documents/GitHub/petstore.txt --bbTargetUrl http://localhost:8080 --outputFormat JAVA_JUNIT_5 --outputFolder ./evomaster-tests --maxTime 30s --ratePerMinute 60 

--------------------------------------------------

DONE:

Ver si corren los tests de xml básicos de evomaster
Agregar mas endpoints mas complejos
Buscar un endpoint en apis guru que requiera objeto xml o acepte.

--------------------------------------------------

DONE:

Benchmark evomaster xml
Hacer test unit de getValueAsPrintableString
Traer a master los commits de evo. y compilar mi version con los cambios de evomaster al dia.
Hacer pr de mi branch a mi master, con review de jp.

--------------------------------------------------


java -jar core/target/evomaster.jar  --blackBox true --bbSwaggerUrl file:///C:/Users/Usuario/Documents/GitHub/SchemaJsonPatch.json --bbTargetUrl http://localhost:8080 --outputFormat JAVA_JUNIT_5 --outputFolder ./evomaster-tests --maxTime 30s --ratePerMinute 60


mvn test -pl :evomaster-e2e-tests-spring-rest-openapi-v3


mvn test -pl :evomaster-core -Dtest=ObjectGeneTest -X

mvn test -pl :evomaster-core -Dtest=ObjectGeneTest -DtrimStackTrace=false


-----


que puede mutar de un objeto json PAtch?

para que tome un cambio de print, hay que recompilar todo!


@XmlRootElement(name = "project")
@XmlAccessorType(XmlAccessType.FIELD)
open class Project(
    @XmlAttribute
    var code: String = "",
    @field:XmlElement(name = "employee", namespace = "")
    var members: List<Member> = mutableListOf()
)
