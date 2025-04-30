
# ParseLocationFromNaturalLanguage

A small Python module that uses a large language model (LLM) to extract and normalize a list of country names from free-form, natural-language region descriptions.

---

## Features

- **Single-step parsing**  
  Converts phrases like “rich Europe and rich EMEA countries” directly into a flat list of country names.  
- **Configurable LLM backend**  
  Defaults to OpenAI’s API but can be extended to other LLM providers.  
- **Lightweight dependency**  
  Only requires the `openai` Python package (or your provider’s SDK) and this module.

---

## Installation

1. Copy `ParseLocationFromNaturalLanguage.py` into your project.  
2. Install dependencies:
   ```bash
   pip install ParseLocationFromNaturalLanguage
   ```

---

## Configuration

Set your OpenAI API key (or other LLM credentials) in the environment:
```bash
export OPENAI_API_KEY="your-api-key"
```

---

## Usage

```python
from ParseLocationFromNaturalLanguage import llm_based_location_parser

# Example 1: return_ISO_NAME_dict=False
query = "all rich countries in Europe and EMEA"
countries = llm_based_location_parser(query, return_ISO_NAME_dict=False, result_language="english")
print(countries)
# -> ["United Kingdom", "Germany", "France", "Italy", "United Arab Emirates", "Saudi Arabia", ...]

# Example 2: return_ISO_NAME_dict=True
iso_countries = llm_based_location_parser(
    query,
    return_ISO_NAME_dict=True,
    result_language="english"
)
print(iso_countries)
# -> {
#      "GB": "United Kingdom",
#      "DE": "Germany",
#      "FR": "France",
#      "IT": "Italy",
#      "AE": "United Arab Emirates",
#      "SA": "Saudi Arabia",
#      ...
#    }
```

---

**Returns:**  
- If `return_ISO_NAME_dict=False`, a list of ISO-standard country names.  
- If `return_ISO_NAME_dict=True`, a dictionary mapping each country’s ISO 3166-1 alpha-2 code to its name.

---
