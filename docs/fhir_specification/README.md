# FHIR Specification Documentation

This directory contains documentation related to FHIR (Fast Healthcare Interoperability Resources) specifications and standards.

## Overview

FHIR is a standard for health information exchange, developed by HL7. It defines how healthcare information can be exchanged between different computer systems regardless of how it is stored in those systems.

## Key FHIR Concepts

### Resources
FHIR defines a set of resources that represent granular clinical concepts:
- **Patient**: Demographics and administrative information
- **Encounter**: Healthcare interactions and visits  
- **Observation**: Measurements, findings, and assessments
- **Condition**: Problems, diagnoses, and health concerns
- **MedicationRequest**: Prescriptions and medication orders
- **ServiceRequest**: Orders for services like lab tests and procedures

### Bundles
Bundles are containers that group related resources together into a single document for exchange.

### References
Resources can reference other resources to establish relationships and context.

### Coding Systems
FHIR uses standardized coding systems like:
- **SNOMED CT**: Clinical terms and concepts
- **LOINC**: Laboratory and clinical observations
- **ICD-10**: Diagnoses and procedures
- **RxNorm**: Medications and drug products

## FHIR R4 Compliance

The scribe2fhir SDK generates FHIR R4 compliant resources and bundles:
- All required fields are populated
- Appropriate extensions are used for additional data
- References maintain referential integrity
- Bundles follow proper structure and metadata

## Resource Mapping

### Clinical Documentation → FHIR Resources
- Patient information → **Patient** resource
- Healthcare visit → **Encounter** resource  
- Symptoms and complaints → **Observation** resources (category: survey)
- Vital signs → **Observation** resources (category: vital-signs)
- Lab results → **Observation** resources (category: laboratory)
- Physical exam → **Observation** resources (category: exam)
- Medical conditions → **Condition** resources
- Prescriptions → **MedicationRequest** resources
- Medication history → **MedicationStatement** resources
- Test orders → **ServiceRequest** resources
- Family history → **FamilyMemberHistory** resources
- Allergies → **AllergyIntolerance** resources
- Immunizations → **Immunization** resources
- Follow-up appointments → **Appointment** resources
- Patient advice → **CarePlan** resources
- Clinical notes → **Communication** resources

## Implementation Notes

The scribe2fhir SDK abstracts FHIR complexity while maintaining compliance:
- Automatic resource ID generation and reference management
- Proper category and status assignments
- Extension usage for additional clinical data
- Validation of required fields and data types

## References
- [FHIR R4 Specification](https://www.hl7.org/fhir/R4/)
- [FHIR Resource Definitions](https://www.hl7.org/fhir/R4/resourcelist.html)
- [FHIR Implementation Guide](https://www.hl7.org/fhir/R4/implementationguide.html)
