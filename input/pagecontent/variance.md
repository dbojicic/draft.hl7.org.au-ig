The HL7 Australia FHIR Working Group has introduced a [Proposal: AU Base & AU Core Variance process](https://confluence.hl7.org/pages/viewpage.action?pageId=227217286). This proposal sets expectations for all HL7 AU FHIR implementation guides to 
- be compliant with AU Core profiles. Implementation guides that are unable to comply with AU Base Core profiles are expected to document these variances.
- to be compliant with AU Base profiles and extensions. Implementation guides that are unable to comply with AU Base profiles or reuse AU Base extensions are expected to document these variances.

To be compliant with an AU Core profile implies that the profiles within the downstream implementation guides satisfy the expectations established by AU Core profile. Instances that are valid against the downstream implementation guide profile are also automatically valid the AU Core profile. Compliance expectations are set at [profile only support](general-requirements.html#profile-only-support), ensuring systems build and conform to defined profiles for data representation without the requirement to implement AU Core interactions. It is important to note that stating compliance with AU Core profiles does not guarantee full conformance.  

### Documenting variance

-  state the version of AU Base or AU Core the variance is related to. 
- list all FHIR artefacts (such as profiles, extensions, and terminology) defined in the downstream implementation guide. The artefacts are listed by their title hyperlinked to its definition.
- document each variance: 
  - for every artefact listed, detail the variance. This should include the specific reasons why the AU Core profile, AU Base extension or AU Base data type profile cannot be used as is. 
  - if an artifact is fully compliant with the existing AU Base profiles, clearly state this compliance as a confirmation of alignment.
- when choosing not to use an AU Base extension, document the reasons why this extension does not meet the needs of your IG, including any limitations or mismatches with the supported use cases.
- if a variance involves data type profiles from AU Base, outline why these profiles are not suitable, detailing the specific requirements of your use case that caused the variance.

#### Types of variances

Examples of the expected types of variances are included below:
- cardinality changes where a downstream profile relaxes cardinality rules set in AU Base or AU Core profile. For example, a Patient profile in a downstream IG allows multiple Medicare numbers by setting the `Patient.identifier:medicare` slice cardinality to 0..* where the cardinality in [AU Core Patient](https://build.fhir.org/ig/hl7au/au-fhir-core/StructureDefinition-au-core-patient.html) profile is 0..1. 
- terminology changes such as including additional codes in a predefined value set to cover more use cases
- removal of Must Support from elements that are flagged as Must Support in AU Core profile

**What is not considered a variance?**

Not all differences from a base specification or profile qualify as a variance. Specifically, an HL7 AU profile that meets the expectations set by its base definition in AU Base or AU Core and adds additional rules on top of these expectations to meet a specific use case. 

Some examples of differences that would not be classified as a variance:

- constrained cardinality. For example, `AllergyIntolerance.code` cardinality in [AU Core AllergyIntolerance](https://build.fhir.org/ig/hl7au/au-fhir-core/StructureDefinition-au-core-allergyintolerance.html) profile has been changed from 0..1 in [AU Base AllergyIntolerance](https://build.fhir.org/ig/hl7au/au-fhir-base/StructureDefinition-au-allergyintolerance.html) to 1..1. 
- increased terminology binding strength. For example, terminology binding strength on `Condition.code` element in [AU Core Condition](https://build.fhir.org/ig/hl7au/au-fhir-core/StructureDefinition-au-core-condition.html) has been changed from [preferred](https://hl7.org/fhir/R4/terminologies.html#preferred) in [AU Base Condition](https://build.fhir.org/ig/hl7au/au-fhir-base/StructureDefinition-au-condition.html) to [extensible](https://hl7.org/fhir/R4/terminologies.html#extensible).  
- added extensions that are officially defined within the FHIR standard.
- added Must Support to elements that are not in scope for AU Core.


_AU Base variance section example_

<div class="bg-success" markdown="1">
**Variance from AU Base**<br><br>
A summary of variances from profiles defined in this implementation guide and profiles in AU Base FHIR implementation guide version 4.2.0-preview. 
- TBD
</div>


_AU Base variance section: HL7 AU eRequesting FHIR IG asserting no variances from AU Base_

<div class="bg-success" markdown="1">
**Variance from AU Base**<br><br>
A summary of variances from profiles defined in this implementation guide and profiles in AU Base FHIR implementation guide version 4.2.0-preview.
- [Diagnostic Service Requesting Base](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnostic-request-base.html): No variance
- [Diagnostic Service Requesting Pathology](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnosticrequest-pathology.html): No variance
- [Diagnostic Service Requesting Radiology](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnosticrequest-radiology.html): No variance
- [Diagnostic Task Base](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-task-base.html): Not in AU Base
- [Diagnostic Requesting Task](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-task-request.html): Not in AU Base
</div>


_AU Core variance section example: HL7 AU Provider Directory FHIR IG documenting non-compliance with AU Core_ 

<div class="bg-success" markdown="1">
**Variance from AU Core**<br><br>
A summary of variances between profiles defined in this implementation guide and profiles defined in AU Core FHIR IG version 0.3.0-ballot.
- [AU PD Practitioner Role](https://build.fhir.org/ig/hl7au/au-fhir-core/StructureDefinition-au-pd-practitionerrole.html): Variance from AU Core PractitionerRole. Unable to use AU Core PractitionerRole profile as it supports 0..1 Medicare Provider Number identifier sliced. Provider Directory has a requirement to support multiple Medicare Provider Numbers.   
</div>


_AU Core variance section example: HL7 AU eRequesting FHIR IG asserting documenting no variances example_

<div class="bg-success" markdown="1">
**Variance from AU Core** <br><br>
A summary of variances between profiles defined in this implementation guide and profiles defined in AU Core FHIR IG version 0.3.0-ballot.
- [Diagnostic Service Requesting Base](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnostic-request-base.html): Not in AU Core
- [Diagnostic Service Requesting Pathology](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnosticrequest-pathology.html): Not in AU Core
- [Diagnostic Service Requesting Radiology](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnosticrequest-radiology.html): Not in AU Core
- [Diagnostic Task Base](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-task-base.html): Not in AU Core
- [Diagnostic Requesting Task](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-task-request.html): Not in AU Core
</div>