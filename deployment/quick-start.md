---
description: Fast non-production Deployment
---

# Quick Start

In order to run Dromon with an in-memory, volatile database, just execute the following:

## Docker

```text
docker run -p 8080:8080 samply/dromon:0.7.0
```

## Java

Dromon works with Java 8 or Java 11.

```text
wget https://github.com/samply/dromon/releases/download/v0.7.0/dromon-0.7.0-standalone.jar
java -jar dromon-0.7.0-standalone.jar -m dromon.core
```

Logging output should appear which prints the most important settings and system parameters like Java version and available memory.

Dromon provides a [FHIR RESTful API](https://www.hl7.org/fhir/http.html) under `http://localhost:8080/fhir`. A good start is to query the [CapabilityStatement](https://www.hl7.org/fhir/capabilitystatement.html) of Dromon using [jq](https://stedolan.github.io/jq/) to select only the software key of the JSON output:

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

Continue with importing your first data:

{% page-ref page="../importing-data.md" %}

