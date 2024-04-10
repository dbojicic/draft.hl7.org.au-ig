<div class="stu-note" markdown="1">
The HL7 Australia FHIR Working Group has introduced a [Proposal: AU Base & AU Core Variance process](https://confluence.hl7.org/pages/viewpage.action?pageId=227217286) that sets expectations for all HL7 AU FHIR implementation guides to:
- be compliant with AU Core profiles. Implementation guides that are unable to comply with AU Base Core profiles are expected to document these variances.
- to be compliant with AU Base profiles and extensions. Implementation guides that are unable to comply with AU Base profiles or reuse AU Base extensions are expected to document these variances.

To be compliant with an AU Core profile implies that the profiles within the downstream implementation guides satisfy the expectations established by AU Core profile. Instances that are valid against the downstream implementation guide profile are automatically valid against the AU Core profile. Compliance expectations are set at [profile only support](general-requirements.html#profile-only-support), ensuring systems build and conform to defined profiles for data representation without the requirement to implement AU Core interactions. It is important to note that stating compliance with AU Core profiles does not guarantee full conformance.

To be compliant with AU Base, instances that are valid against downstream implementation guide profiles are, by default, considered compliant with the AU Base profile.

The AU Base and AU Core variance process is currently being developed. Guidance provided here is subject to change as the process matures.
</div>

### Documenting variance

To document a variance in an implementation guide: 

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

#### No variance from AU Base
Where you have no variance from AU Base, insert this statement:

>This implementation guide has no variance from AU Base FHIR implementation guide version (insert version here).  

_AU Base variance example:A FHIR IG asserts no variance against the AU Base_

<div class="bg-success" markdown="1">
**Variance from AU Base**<br><br>
This implementation guide has no variance from AU Base FHIR implementation guide version 4.2.0-preview.  
</div>

#### Variance from AU Base
Where you have a variance from AU Base, document the variance and reasons why the AU Base profile , extension, or  AU Base data type profile cannot be used as is. 

_AU Base variance section example: A FHIR IG documents variance from AU Base_ 
<div class="bg-success" markdown="1">
**Variance from AU Base**<br><br>
A summary of variances between profiles defined in this implementation guide and profiles defined in AU Base FHIR IG version 4.2.0-preview.
- [AU FHIR IG profile 1](profile1.html): TBD
</div>

#### No variance from AU Core 
Where you have no variance from AU Core, insert this statement: 

>This implementation guide has no variance from AU Core FHIR implementation guide version (insert version here). 

_AU Base variance example:A FHIR IG asserts no variance against the AU Base_

<div class="bg-success" markdown="1">
**Variance from AU Core**<br><br>
This implementation guide has no variance from AU Core FHIR implementation guide version 0.3.0-ballot.  
</div>
#### Variance from AU Core
Where you have a variance from AU Core, document the variance and reasons why the AU Core profile cannot be used as is.

_AU Core variance section example: A FHIR IG documents variance from AU Core_

<div class="bg-success" markdown="1">
**Variance from AU Core**<br><br>
A summary of variances between profiles defined in this implementation guide and profiles defined in AU Base FHIR IG version 4.2.0-preview.
- [AU PractitionerRole Profile](practitionerrole-profile.html): Variance from AU Core PractitionerRole.
  - Relaxed cardinality: PractitionerRole.identifier:medicareProvider cardinality is 0..*. Unable to use AU Core PractitionerRole profile as it supports 0..1 Medicare Provider Number identifier slices.
  - Removed Must Support: PractitionerRole.location
</div>

#### Profiles not in AU Base or AU Core

For FHIR implementation guides that introduce profiles not present in AU Base or AU Core Implementation Guides, the HL7 FHIR Working Group recommends listing all of these profiles. This will assists in identifying  potential profiles for the FHIR Working Group to develop further.

_Example: A FHIR IG provides a list of profiles not included in AU Base_
<div class="bg-success" markdown="1">
**Additional profiles**<br><br>
Profiles in this implementation guide that are not in AU Base FHIR Implementation Guide version 4.2.0-preview:
- [Diagnostic Task Base](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-task-base.html)
- [Diagnostic Requesting Task](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-task-request.html)
</div>

_Example: A FHIR IG provides a list of profiles not included in AU Core
<div class="bg-success" markdown="1">
**Additional profiles**<br><br>
Profiles in this implementation guide that are not in AU Core FHIR IG version 0.3.0-ballot:
- [Diagnostic Service Requesting Base](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnostic-request-base.html)
- [Diagnostic Service Requesting Pathology](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnosticrequest-pathology.html)
- [Diagnostic Service Requesting Radiology](https://build.fhir.org/ig/hl7au/au-fhir-erequesting/branches/scaffold/StructureDefinition-erequesting-diagnosticrequest-radiology.html)
</div>