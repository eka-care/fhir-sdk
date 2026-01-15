# Objective Backlinking Documentation

This directory contains documentation about objective backlinking and cross-referencing within FHIR documents.

## Overview

Objective backlinking refers to the systematic creation and maintenance of references between related FHIR resources within a bundle. This ensures that clinical information maintains proper relationships and context.

## Reference Types in scribe2fhir

### Patient References
- **Used by**: All clinical resources (Observations, Conditions, MedicationRequests, etc.)
- **Purpose**: Links clinical data to the specific patient
- **Format**: `Patient/{patient-id}`

### Encounter References  
- **Used by**: Clinical activities during an encounter
- **Purpose**: Associates clinical data with a specific healthcare interaction
- **Format**: `Encounter/{encounter-id}`

### Condition References
- **Used by**: MedicationRequests (reason for prescription)
- **Purpose**: Links treatments to the conditions they address
- **Format**: `Condition/{condition-id}`

## Automatic Reference Management

The scribe2fhir SDK automatically manages references:

```python
builder = FHIRDocumentBuilder()

# 1. Create patient - establishes patient context
patient = builder.add_patient(name="John Doe")

# 2. Create encounter - establishes encounter context  
encounter = builder.add_encounter()

# 3. All subsequent resources automatically reference patient and encounter
symptom = builder.add_symptom(code="Headache")  # → References patient and encounter
condition = builder.add_condition(code="Migraine")  # → References patient and encounter
medication = builder.add_medication_prescribed(code="Sumatriptan")  # → References patient and encounter
```

## Reference Consistency

### Within Bundle Validation
- All references point to resources that exist within the same bundle
- Reference formats follow FHIR specifications
- Display names are populated for human readability

### Cross-Resource Relationships
```python
# Condition established in medical history
condition = builder.add_medical_condition_history(code="Hypertension")

# Medication prescribed for the condition  
medication = builder.add_medication_prescribed(
    medication="Lisinopril",
    reason="Hypertension"  # Links to condition
)

# Lab test ordered to monitor condition
lab_order = builder.add_test_prescribed(
    code="Basic Metabolic Panel",
    reason="Hypertension monitoring"
)

# Follow-up scheduled for condition management
followup = builder.add_followup(
    date="2024-06-01",
    notes="Blood pressure recheck for hypertension"
)
```

## Reference Integrity

### Automatic ID Generation
- Every resource receives a unique UUID
- IDs are consistent throughout the bundle
- References use the generated IDs automatically

### Reference Display Names
- Patient references include patient name for readability
- Encounter references include encounter type when available
- Condition references include condition name

## Bundle Structure

### Resource Ordering
Resources appear in bundles in creation order:
1. Patient (if added)
2. Encounter (if added)
3. Clinical resources (Observations, Conditions, etc.)
4. Supporting resources (Appointments, CarePlans, Communications)

### Reference Resolution
- **Internal references**: Point to resources within the same bundle
- **External references**: Can point to resources in other systems (future enhancement)
- **Contained resources**: Inline resources when appropriate

## Clinical Context Propagation

### Patient Context
Once a patient is added, all subsequent resources automatically:
- Include patient reference in `subject` field
- Use patient name in reference display
- Maintain patient ID consistency

### Encounter Context  
Once an encounter is added, applicable resources automatically:
- Include encounter reference in `encounter` field
- Associate with the healthcare interaction
- Support encounter-based reporting

## Advanced Reference Scenarios

### Multiple Encounters
```python
# Current implementation supports one encounter per builder
# For multiple encounters, use separate builders or document context switching
encounter1 = builder.add_encounter(encounter_type="Initial visit")
# ... add resources for first encounter ...

# Switch to new builder for second encounter
builder2 = FHIRDocumentBuilder()
builder2.add_patient(name="John Doe")  # Same patient
encounter2 = builder2.add_encounter(encounter_type="Follow-up visit")
# ... add resources for second encounter ...
```

### Cross-Reference Validation
The SDK validates that:
- Referenced resources exist in the bundle
- Reference formats are valid FHIR
- Required references are present
- Circular references are avoided

## Reference Examples

### Patient Reference
```json
{
  "subject": {
    "reference": "Patient/12345678-1234-1234-1234-123456789012",
    "display": "John Doe"
  }
}
```

### Encounter Reference
```json
{
  "encounter": {
    "reference": "Encounter/87654321-4321-4321-4321-210987654321",
    "display": "Office Visit"
  }
}
```

### Condition Reference (in MedicationRequest)
```json
{
  "reasonReference": [
    {
      "reference": "Condition/11223344-5566-7788-9900-aabbccddeeff",
      "display": "Hypertension"
    }
  ]
}
```

## Best Practices

### Reference Management
1. Always add patient first to establish context
2. Add encounter before clinical activities when applicable  
3. Let the SDK manage references automatically
4. Use consistent patient information across builders if using multiple
5. Validate bundle references before external sharing

### Clinical Relationships
1. Link medications to conditions when prescribing for specific diagnoses
2. Associate lab orders with monitoring requirements
3. Connect follow-up appointments to ongoing conditions
4. Reference diagnostic findings in treatment decisions

## Future Enhancements

### Planned Features
- External reference support for multi-bundle scenarios
- Reference validation utilities
- Cross-bundle reference resolution
- Advanced relationship modeling

## Notes
- Reference management is handled transparently by the SDK
- Manual reference creation is possible but not recommended
- Bundle validation ensures reference integrity
- Reference patterns follow FHIR best practices automatically
