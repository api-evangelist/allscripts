---
name: veradigm-fhir-patient-summary
description: Retrieve a patient's core clinical summary (demographics, conditions, medications,
  allergies, observations) from the Veradigm FHIR R4 API using SMART on FHIR authorization.
api: Veradigm FHIR R4 API
operations:
- Patient.read
- Patient.search-type
- Condition.search-type
- MedicationRequest.search-type
- AllergyIntolerance.search-type
- Observation.search-type
generated: '2026-08-14'
method: generated
source: conformance/allscripts-fhir-r4-capabilitystatement.json (live CapabilityStatement),
  scopes/allscripts-scopes.yml, errors/allscripts-problem-types.yml
---

# Veradigm FHIR Patient Clinical Summary

Pull together a patient's core clinical picture from the Veradigm FHIR R4 API: demographics,
active conditions, current medications, allergies, and recent observations. Every operation below
maps to a resource type + interaction Veradigm's own server actually declares in its live
CapabilityStatement (`conformance/allscripts-fhir-r4-capabilitystatement.json`) — none are
invented.

## Prerequisites

1. A registered FHIR application in the Veradigm Connect portal
   (https://developer.veradigm.com/), App Type `Patient` or `Provider`.
2. An OAuth 2.0 access token obtained via SMART on FHIR (standalone or EHR launch). See
   `authentication/allscripts-authentication.yml`.
3. Scopes for each resource you intend to read — at minimum
   `patient/Patient.read patient/Condition.rs patient/MedicationRequest.rs
   patient/AllergyIntolerance.rs patient/Observation.rs`. Full scope catalog in
   `scopes/allscripts-scopes.yml`.
4. The tenant's FHIR base URL, resolved from the Veradigm Endpoint Directory
   (https://developer.veradigm.com/Fhir/EndpointDirectory) — this is NOT a single fixed host;
   each client organization has its own base.

## Steps

1. **Confirm server capabilities.** GET `{base}/metadata` and check the CapabilityStatement for
   the resource types and interactions you need (`rest.resource[].interaction[].code`). Do not
   assume a resource is available — some tenants run older Veradigm EHR versions with a smaller
   supported set (see `lifecycle/allscripts-lifecycle.yml`).
2. **Resolve the patient.** GET `{base}/Patient/{id}` (interaction: `read`) if you already have
   the FHIR id from the SMART launch context, or GET `{base}/Patient?_id={id}` (interaction:
   `search-type`) otherwise.
3. **Pull active conditions.** GET
   `{base}/Condition?patient={patientId}&clinical-status=active` (interaction: `search-type`,
   reference searchParam `patient` per the live CapabilityStatement — see
   `data-model/allscripts-data-model.yml`).
4. **Pull current medications.** GET `{base}/MedicationRequest?patient={patientId}&status=active`
   (interaction: `search-type`).
5. **Pull allergies.** GET `{base}/AllergyIntolerance?patient={patientId}` (interaction:
   `search-type`).
6. **Pull recent vitals/labs.** GET
   `{base}/Observation?patient={patientId}&category=http://terminology.hl7.org/CodeSystem/observation-category|vital-signs`
   and repeat with `|laboratory` for labs — these are real category-scoped SMART scopes
   (`patient/Observation.rs?category=...`), not generic wildcards. See
   `scopes/allscripts-scopes.yml`.
7. **Paginate.** Each search response is a `Bundle` with a `link[]` array (`self`/`next`); follow
   `next` until absent. See `conventions/allscripts-conventions.yml`.
8. **Handle errors.** 401 = missing/invalid token; 403 = token valid but scope insufficient; 404 =
   resource/tenant not found; 413 = result set too large, narrow your search. A response may also
   come back with content explicitly marked "redacted" rather than a 403 — treat that as "data
   exists but you're not authorized to view it," not as an empty result. See
   `errors/allscripts-problem-types.yml`.

## Notes

- This surface has no OpenAPI document; every field/parameter name above should be cross-checked
  against the live `/metadata` CapabilityStatement for the specific tenant you're calling, since
  supported resources vary by Veradigm EHR version.
- Bulk, multi-patient extraction is a **separate**, asynchronous flow (System app type + JWKS
  auth only) — do not attempt to loop this per-patient flow across a population. See
  `sandbox/allscripts-sandbox.yml` and the Bulk Data docs.
