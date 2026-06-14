# Allscripts (Veradigm) GraphQL Schema

## Overview

This conceptual GraphQL schema represents the Allscripts (Veradigm) healthcare EHR APIs, covering the Veradigm FHIR R4 API and the Veradigm Unity API. Allscripts, now operating under the Veradigm brand, provides REST and FHIR-based APIs for EHR data exchange, clinical workflows, patient portal integration, and practice management. The Unity API supports both SOAP and REST endpoints across Allscripts EHR product lines including Touchworks, Professional EHR, and Paragon acute care solutions.

The schema unifies the domain objects surfaced by these APIs into a single typed graph, enabling developers to reason about patients, encounters, medications, orders, clinical documents, scheduling, billing, and interoperability resources in one coherent model.

## Source APIs

- **Veradigm FHIR R4 API** — `https://open.platform.veradigm.com` — FHIR R4-compliant access to 28 clinical resources including Patient, Condition, Observation, MedicationRequest, and Encounter. Uses OAuth 2.0 with SMART on FHIR 2.0.
- **Veradigm Unity API** — `https://remotecentral.allscripts.com` — Action-based dispatch model providing read-write access to clinical, scheduling, demographic, and practice management data across Allscripts EHR product lines.
- **Veradigm Paragon Open API** — FHIR-compliant access to acute care EHR data from the Paragon platform.

## Developer Resources

- Developer Portal: https://developer.veradigm.com/
- Legacy Developer Portal: https://developer.allscripts.com/
- FHIR Introduction: https://developer.veradigm.com/Fhir/Introduction
- FHIR Sandbox: https://developer.veradigm.com/Fhir/FHIR_Sandboxes
- Unity API Docs: https://developer.allscripts.com/
- App Expo (partner app marketplace): https://expo.veradigm.com/apps
- Sign Up: https://developer.veradigm.com/Content/fhir/content/Developer_Signup/
- Terms of Service: https://veradigm.com/legal/terms-of-use/

## Schema Design Notes

The schema models the following domain areas:

### Patient & Demographics
`Patient`, `PatientDetails`, `PatientDemographics`, and `PatientContact` capture the core identity, demographic, and contact information surfaced by the FHIR Patient resource and the Unity API's GetPatient and SearchPatients actions. `PatientInsurance` represents coverage and payer data associated with a patient record.

### Clinical Encounters
`Encounter`, `EncounterDetails`, `EncounterType`, and `EncounterStatus` map to FHIR Encounter resources and Unity API encounter data. Encounters link patients to providers, locations, diagnoses, procedures, and orders.

### Diagnoses & Coding
`Diagnosis`, `DiagnosisDetails`, `DiagnosisCode`, `ICD10`, and `ICD11` represent the FHIR Condition resource and problem list entries. Both ICD-10 and ICD-11 coding systems are modeled to support current and forward-looking implementations.

### Medications & Orders
`MedOrder`, `Medication`, `MedicationDetails`, `MedicationRoute`, `MedicationDosage`, and `MedicationSig` cover the FHIR MedicationRequest and MedicationStatement resources, as well as Unity API medication and prescription actions. `ConnectRx` represents the Allscripts e-prescribing integration layer.

### Allergies
`Allergy`, `AllergyDetails`, and `AllergyStatus` map to the FHIR AllergyIntolerance resource and Unity API allergy data, capturing substance, reaction, severity, and clinical status.

### Procedures & CPT Coding
`Procedure`, `ProcedureDetails`, `CPT`, and `ProcedureStatus` represent FHIR Procedure resources and procedural documentation, with CPT code support for billing integration.

### Laboratory
`Lab`, `LabOrder`, `LabResult`, and `LabResultValue` cover the FHIR DiagnosticReport and Observation resources for laboratory data, supporting ordered labs, resulted values, reference ranges, and interpretations.

### Imaging
`Imaging`, `ImagingOrder`, and `ImagingResult` represent the FHIR ImagingStudy resource and diagnostic imaging workflows, including DICOM integration points.

### Clinical Documents
`Document` and `DocumentDetails` map to FHIR DocumentReference and ClinicalDocument resources, supporting C-CDA, clinical notes, discharge summaries, and other structured documents.

### Scheduling & Appointments
`Appointment`, `AppointmentDetails`, `AppointmentType`, `AppointmentStatus`, `Schedule`, and `SlotDetails` cover the FHIR Appointment and Schedule resources alongside Unity API scheduling actions for booking, modifying, and querying provider availability.

### Providers & Practices
`Provider`, `ProviderDetails`, `ProviderCredentials`, `Practice`, `PracticeDetails`, and `Location` represent the FHIR Practitioner, Organization, and Location resources, as well as Unity API provider and enterprise data.

### Claims & Billing
`Claim` and `ClaimDetails` surface billing and claims data, linking clinical encounters and procedures to payer information.

### FHIR & HL7 Interoperability
`FHIR`, `FHIRResource`, and `HL7` provide generic interoperability wrappers for FHIR R4 resource bundles and HL7 message structures used in the Veradigm ecosystem.

### Authentication & Access
`APIKey`, `Token`, and `Webhook` represent the OAuth 2.0 / SMART on FHIR authentication artifacts, access tokens, and event-driven notification subscriptions supported by the Veradigm developer platform.

## GraphQL Schema File

See `allscripts-schema.graphql` for the full type definitions.
