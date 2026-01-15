# scribe2fhir Repository

A multi-language SDK for creating FHIR documents from clinical data.

## Repository Structure

```
scribe2fhir/
├── docs/                           # Repository-wide documentation
│   ├── fhir_specification/         # FHIR standard documentation
│   └── objective_backlinking/      # Objective backlinking documentation
├── python/                         # Python SDK implementation
│   ├── scribe2fhir/               # Python package
│   │   ├── core/                  # Core SDK functionality
│   │   └── __init__.py
│   ├── docs/                      # Python-specific documentation
│   ├── tests/                     # Python test suite
│   ├── requirements.txt           # Python dependencies
│   ├── setup.py                   # Python package setup
│   └── example_usage.py           # Usage examples
└── [future_language]/             # Future language implementations
    ├── core/
    ├── docs/
    └── tests/
```

## Language Implementations

### Python SDK
The Python implementation is located in the `python/` directory and provides:

- **scribe2fhir.core**: Main SDK package
- **Comprehensive documentation**: Element-by-element usage guides
- **Full test suite**: 165+ test methods covering all functionality
- **Example code**: Real-world usage examples

#### Quick Start (Python)
```bash
cd python/
pip install -r requirements.txt
pip install -e .
```

```python
from scribe2fhir.core import FHIRDocumentBuilder
from scribe2fhir.core.types import create_codeable_concept

builder = FHIRDocumentBuilder()
builder.add_patient(name="John Doe", age=30, gender="male")
fhir_json = builder.convert_to_fhir()
```

### Future Language Implementations
Additional language SDKs will follow the same structure:
- `javascript/` - Node.js/TypeScript implementation
- `java/` - Java implementation  
- `csharp/` - C# implementation
- `go/` - Go implementation

## Documentation Structure

### Repository-level Documentation (`docs/`)
- **FHIR Specification**: Standards and compliance documentation
- **Objective Backlinking**: Cross-referencing and relationship documentation

### Language-specific Documentation (`{language}/docs/`)
- Element-by-element usage guides
- API reference documentation  
- Integration examples
- Best practices

## Contributing
Each language implementation follows consistent patterns:
1. **Core library** in `{language}/core/`
2. **Comprehensive tests** in `{language}/tests/`
3. **Documentation** in `{language}/docs/`
4. **Package configuration** in language-appropriate files

## License
MIT License - see LICENSE file for details.

## Support
- Documentation: See language-specific docs folders
- Issues: GitHub issues for bug reports and feature requests
- Community: Discussion forums for usage questions
