# Allscripts (Veradigm)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Allscripts, now operating as Veradigm (rebranded January 2023), is a healthcare IT company providing APIs for EHR data exchange, clinical workflows, patient portal, and practice management integrations. The Veradigm Developer Program (formerly Allscripts Developer Program) offers access to FHIR R4 and Unity APIs through a tiered subscription model.

## APIs

### Veradigm FHIR R4 API
RESTful access to 28 FHIR R4 clinical resources including Patient, Condition, Observation, MedicationRequest, Encounter, AllergyIntolerance, DiagnosticReport, and more. Uses OAuth 2.0 with SMART on FHIR Application Launch Framework 2.0. Supports both patient-facing (ending in /open) and provider-facing (ending in /fhir) endpoints.

- Documentation: https://developer.veradigm.com/Fhir/Introduction
- Supported Resources: https://developer.veradigm.com/Fhir/Resources
- Endpoint Directory: https://developer.veradigm.com/Fhir/EndpointDirectory
- Sandbox: https://developer.veradigm.com/Fhir/FHIR_Sandboxes

### Veradigm Unity API
Read-write access to clinical, scheduling, demographic, and practice management data across Allscripts EHR products (Touchworks, Professional EHR, acute care). Supports REST/JSON and SOAP/XML via an action-based dispatch model.

- Developer Portal: https://developer.allscripts.com/
- Unity EULA: https://veradigm.com/img/legal/pm/Unity-API-EULA.pdf

### Veradigm Paragon Open API
FHIR-compliant API for the Paragon acute care EHR platform, enabling third-party integrations for hospital and acute care settings.

- Documentation: https://developer.veradigm.com/Content/fhir/paragon/ParagonOpenAPI_Index.html

## Developer Program

The Veradigm Connect developer program offers five integrator tiers:

| Tier | Use Case |
|------|----------|
| Open (Free) | Exploration and sandbox testing |
| Bronze | Early development |
| Silver | Prototyping |
| Gold | Production clinical integrations |
| Platinum | Scaling with dedicated support |
| Platinum Plus | Strategic partnership |

Annual billing provides a 10% discount. Sign up at https://developer.veradigm.com/Content/fhir/content/Developer_Signup/

## Links

- Developer Portal: https://developer.veradigm.com/
- App Expo: https://expo.veradigm.com/apps
- API Workshop: https://lp.veradigm.com/api-workshop-registration-april
- Legal: https://veradigm.com/legal/
- Contact: VeradigmConnect@veradigm.com
