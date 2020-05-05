---
description: In environments without Docker
---

# Manual Deployment

The installation should work under Windows, Linux and MacOS. Both Datomic and Dromon need a current Java 8 JRE. Other Versions of Java aren’t currently tested.

## Datomic

Dromon needs a [Datomic](https://www.datomic.com/) database to store FHIR® resources. Different editions of Datomic are available. Four our use case, the Free Edition is sufficient.

You can download Datomic Free here: [https://my.datomic.com/downloads/free](https://my.datomic.com/downloads/free)

Please download Version 0.9.5703 and unpack the ZIP into a directory of your choice. After that please follow the steps:

* open a terminal and change into the `datomic-free-0.9.5703` dir
* copy the sample properties file located at \(relative\) `config/samples/free-transactor-template.properties` to `config/transactor.properties`
* start the database by calling `bin/transactor config/transactor.properties`

The output should look like this:

```text
Launching with Java options -server -Xms1g -Xmx1g -XX:+UseG1GC -XX:MaxGCPauseMillis=50
Starting datomic:free://localhost:4334/<DB-NAME>, storing data in: data ...
System started datomic:free://localhost:4334/<DB-NAME>, storing data in: data
```

You can change the data dir in the properties file if you like to have it at a different location.

## Dromon

Dromon runs on the JVM and comes as single JAR file. Download the most recent version [here](https://github.com/samply/dromon/releases/tag/v0.7.0). Look for `dromon-0.7.0-standalone.jar`. Dromon requires at least Java 8 and is also tested with Java 11.

After the download, you can start dromon with the following command \(Linux, MacOS\):

```text
DATABASE_URI=datomic:free://localhost:4334/db java -jar dromon-0.7.0-standalone.jar -m dromon.core
```

Under Windows you need to set the Environment variables in the PowerShell before starting Dromon:

```text
$Env:DATABASE_URI = "datomic:free://localhost:4334/db"
java -jar dromon-0.7.0-standalone.jar -m dromon.core
```

The output should look like this:

```text
19-12-16 11:49:18 ce3fb21de517 INFO [dromon.system:165] - Set log level to: info
19-12-16 11:49:18 ce3fb21de517 INFO [dromon.system:43] - Try to read dromon.edn ...
19-12-16 11:49:18 ce3fb21de517 INFO [dromon.system:152] - Feature OpenID Authentication disabled
19-12-16 11:49:18 ce3fb21de517 INFO [dromon.system:74] - Loading namespaces ...
WARNING: requiring-resolve already refers to: #'clojure.core/requiring-resolve in namespace: datomic.common, being replaced by: #'datomic.common/requiring-resolve
19-12-16 11:49:32 ce3fb21de517 INFO [dromon.system:76] - Loaded the following namespaces: dromon.datomic.transaction, dromon.structure-definition, dromon.datomic, dromon.fhir.operation.evaluate-measure, dromon.handler.health, dromon.interaction.history.instance, dromon.interaction.history.system, dromon.interaction.history.type, dromon.interaction.transaction, dromon.interaction.create, dromon.interaction.delete, dromon.interaction.read, dromon.interaction.search-type, dromon.interaction.update, dromon.rest-api, dromon.handler.app, dromon.metrics, dromon.handler.metrics, dromon.server, dromon.thread-pool-executor-collector, dromon.terminology-service.extern, dromon.terminology-service
19-12-16 11:49:33 ce3fb21de517 INFO [dromon.structure-definition:140] - Read structure definitions resulting in: 190 structure definitions
19-12-16 11:49:33 ce3fb21de517 INFO [dromon.datomic:25] - Created database at: datomic:mem://dev
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.datomic:18] - Upsert schema in database: datomic:mem://dev creating 92290 new facts
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.datomic:29] - Connect with database: datomic:mem://dev
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.fhir.operation.evaluate-measure:69] - Init FHIR $evaluate-measure operation executor
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.terminology-service.extern:184] - Init terminology server connection: http://tx.fhir.org/r4
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.fhir.operation.evaluate-measure:63] - Init FHIR $evaluate-measure operation handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.handler.health:21] - Init health handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.history.instance:108] - Init FHIR history instance interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.history.system:122] - Init FHIR history system interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.history.type:125] - Init FHIR history type interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.transaction:396] - Init FHIR transaction interaction executor
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.transaction:390] - Init FHIR transaction interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.create:82] - Init FHIR create interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.delete:62] - Init FHIR delete interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.read:98] - Init FHIR read interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.search-type:126] - Init FHIR search-type interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.interaction.update:113] - Init FHIR update interaction handler
19-12-16 11:49:36 ce3fb21de517 INFO [dromon.rest-api:385] - Init FHIR RESTful API with base URL: http://localhost:8080/fhir
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.handler.app:35] - Init app handler
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.system:199] - Init server executor
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.thread-pool-executor-collector:70] - Init thread pool executor collector.
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.metrics:27] - Init metrics registry
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.handler.metrics:29] - Init metrics handler
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.system:220] - Start metrics server on port 8081
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.system:208] - Start main server on port 8080
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.core:58] - JVM version: 11.0.4
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.core:59] - Maximum available memory: 1490 MiB
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.core:60] - Number of available processors: 4
19-12-16 11:49:37 ce3fb21de517 INFO [dromon.core:61] - Successfully started Dromon version 0.7.0 in 19.4 seconds
```

In order to test connectivity, query the health endpoint:

```text
curl http://localhost:8080/health
```

After that please note that the [FHIR RESTful API](https://www.hl7.org/fhir/http.html) is available under `http://localhost:8080/fhir`. A good start is to query the [CapabilityStatement](https://www.hl7.org/fhir/capabilitystatement.html) of Dromon using [jq](https://stedolan.github.io/jq/) to select only the software key of the JSON output:

```text
curl -H 'Accept:application/fhir+json' -s http://localhost:8080/fhir/metadata | jq .software
```

that should return:

```javascript
{
  "name": "Dromon",
  "version": "0.7.0"
}
```

Dromon will be configured through environment variables which are documented here:

{% page-ref page="environment-variables.md" %}

