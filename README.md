```markdown
# ParseLocationFromNaturalLanguage

A small Python module that uses a large language model (LLM) to extract and normalize a list of country names from free-form, natural-language region descriptions.

---

## Features

- **Single-step parsing**  
  Convert phrases like “rich Europe and rich EMEA countries” directly into a flat list of country names.  
- **Configurable LLM backend**  
  Defaults to OpenAI’s API but can be extended to other LLM providers.  
- **Lightweight dependency**  
  Only requires the `openai` Python package (or your provider’s SDK) and this module.

---

## Installation

1. Copy `ParseLocationFromNaturalLanguage.py` into your project.  
2. Install dependencies:
   ```bash
   pip install openai
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

# Parse a natural-language description into individual country names
query = "all rich countries in Europe and EMEA"
countries = llm_based_location_parser(query)

print(countries)
# e.g. ["United Kingdom", "Germany", "France", "Italy", "United Arab Emirates", "Saudi Arabia", ...]
```

---

## API Reference

### `llm_based_location_parser(text: str, model: str = "gpt-4", temperature: float = 0.0) → List[str]`

| Parameter    | Type    | Description                                                                                   |
| ------------ | ------- | --------------------------------------------------------------------------------------------- |
| `text`       | `str`   | Free-form region description (e.g. “rich Europe and rich EMEA countries”).                    |
| `model`      | `str`   | (Optional) LLM model identifier (default: `"gpt-4"`).                                         |
| `temperature`| `float` | (Optional) Sampling temperature for the LLM (default: `0.0` for deterministic output).       |

**Returns:**  
- A list of ISO-standard country names matching the described regions.

---

## Example

```python
from ParseLocationFromNaturalLanguage import llm_based_location_parser

# Example 1: simple region
print(llm_based_location_parser("countries in Scandinavia"))
# -> ["Sweden", "Norway", "Denmark", "Finland", "Iceland"]

# Example 2: qualifier + region
print(llm_based_location_parser("rich Europe and rich EMEA countries"))
# -> ["United Kingdom", "Germany", "France", "Italy", "United Arab Emirates", "Saudi Arabia", ...]
```

---

## Customizing

- **Switch LLM provider**  
  Replace the OpenAI client calls inside `llm_based_location_parser` with your preferred API.  
- **Region maps**  
  If you need to override or supplement the LLM’s output, post-process the returned list against your own `REGION_MAP`.

---

## Requirements

- Python 3.8+  
- `openai` (or your chosen SDK)

---

## License

MIT © 2025 Your Company Name
```
