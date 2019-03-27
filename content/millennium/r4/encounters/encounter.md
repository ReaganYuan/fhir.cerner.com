---
title: Encounter | R4 API
---

# Encounter

* TOC
{:toc}

## Overview

The Encounter resource provides admissions or visits during which health care services were provided to a patient. An encounter has a class to distinguish between different health care settings such as inpatient, outpatient, emergency, etc. A patient may have one medical record number with multiple encounter numbers per facility or organization. There is substantial variance between organizations in the definition of an encounter and what events are aggregated together to constitute an encounter.

## Search

Search for Encounters that meet supplied query parameters:

    GET /Encounter?:parameters

_Implementation Notes_

* The [Encounter.hospitalization.destination] will be returned as a reference to a [contained] location resource.
* The [Encounter.location.location] may be returned as a reference to a [contained] location resource.

### Authorization Types

<%= authorization_types(practitioner: true, patient: false, system: true)%>

### Parameters

 Name       | Required?                  | Type          | Description
------------|----------------------------|---------------|-------------------------------------------------------------------------------------------------------
 `_id`      | This or patient or subject | [`token`]     | The logical resource id associated with the Encounter. Example: `7891`
 `patient`  | This or subject or _id     | [`reference`] | The patient present at the encounter. Example: `12345`
 `subject`  | This or patient or _id     | [`reference`] | The patient present at the encounter. Example: subject=Patient/1316024 or subject:Patient=1316024
 [`_count`] | No                          | [`number`]    | The maximum number of results to return.

### Headers

 <%= headers %>

### Example

#### Request

    GET https://fhir-open.sandboxcerner.com/r4/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Encounter?patient=4342010

#### Response

<%= headers status: 200 %>
<%= json(:r4_encounter_bundle) %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

## Retrieve by id

List an individual Encounter by its id:

    GET /Encounter/:id

_Implementation Notes_

* The [Encounter.hospitalization.destination] will be returned as a reference to a [contained] location resource.
* The [Encounter.location.location] may be returned as a reference to a [contained] location resource.

### Authorization Types

<%= authorization_types(practitioner: true, patient: false, system: true)%>

### Headers

<%= headers %>

### Example

#### Request

    GET https://fhir-open.sandboxcerner.com/r4/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Encounter/4027918

#### Response

<%= headers status: 200 %>
<%= json(:r4_encounter) %>

### Errors

The common [errors] and [OperationOutcomes] may be returned.

[contained]: http://hl7.org/fhir/R4/references.html#contained
[Encounter.hospitalization.destination]: http://hl7.org/fhir/R4/encounter-definitions.html#Encounter.hospitalization.destination
[Encounter.location.location]: http://hl7.org/fhir/R4/encounter-definitions.html#Encounter.location.location
[`reference`]: http://hl7.org/fhir/R4/search.html#reference
[`token`]: http://hl7.org/fhir/R4/search.html#token
[`number`]: http://hl7.org/fhir/R4/search.html#number
[`_count`]: http://hl7.org/fhir/R4/search.html#count
[errors]: ../../#client-errors
[OperationOutcomes]: ../../#operation-outcomes

## Patch

Patch an existing encounter.

    PATCH /Encounter/:id

_Implementation Notes_

* Only operations on the paths listed below are supported.

### Authorization Types

<%= authorization_types(practitioner: true, system: true) %>

### Headers

<%= headers head: {Authorization: '&lt;OAuth2 Bearer Token>', 'Accept': 'application/fhir+json',
                   'Content-Type': 'application/json-patch+json', 'If-Match': 'W/"&lt;Current version of the Encounter resource>"'} %>

### Patch Operations

<%= patch_definition_table(:encounter_patch, :patch, :r4) %>

### Example

#### Request

    PATCH https://fhir-ehr.sandboxcerner.com/r4/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Encounter/1621910

#### Body

<%= json(:r4_encounter_patch) %>

#### Response

<%= headers status: 200 %>
<pre class="terminal">
    Cache-Control: no-cache
    Content-Length: 0
    Content-Type: text/html
    Date: Tue, 26 Mar 2019 15:42:29 GMT
    Etag: W/"10"
    Last-Modified: Tue, 26 Mar 2019 15:42:27 GMT
    Server-Response-Time: 2260.237021
    Status: 200 OK
    Vary: Origin
    X-Request-Id: 47306a14c8a2c3afd4ab85aa9594101d
    X-Runtime: 2.260092
</pre>

The `ETag` response header indicates the current `If-Match` version to use on subsequent updates.
