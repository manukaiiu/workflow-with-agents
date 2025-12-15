# Protocol: >>add-input

**Trigger**: `>>add-input <path-or-url>` or "here's another document", "add this file"
**Purpose**: Add input source to concept work

---

## Protocol Steps

### 1. Determine Input Type

| Type | Source | Handling |
|------|--------|----------|
| URL | Web page | Fetch content, save locally to 01-INPUTS/ |
| Local file | File path | Copy to 01-INPUTS/ |
| PDF | PDF file | Extract content, confirm accuracy with human |
| Conversation | Chat export | Save to 01-INPUTS/ |
| Document | .md, .txt, etc. | Copy to 01-INPUTS/ |

### 2. Add Entry to INDEX.md

Update `01-INPUTS/INDEX.md`:

```markdown
## [Input Name]
- **Source**: [path or URL]
- **Type**: conversation | document | pdf | web | other
- **Size**: [lines/pages/words estimate]
- **Added**: [date]
- **Status**: [ ] Not processed
- **Processing Notes**: [Any issues or considerations]
- **Summary**: [Brief description - filled after extraction]
```

### 3. Update OVERVIEW

Update `00-OVERVIEW.md`:
- Increment input count
- Add to inputs checklist

### 4. Handle Large Inputs

For inputs 10000+ lines:
- Do NOT summarize or skip content
- Note in INDEX.md: "Large input - will process in chunks"
- Track progress with line ranges during extraction

### 5. Confirm to Human

```
Added input: [Name]
- Source: [path/url]
- Type: [type]
- Size: [estimate]
- Status: Not processed

Updated: 01-INPUTS/INDEX.md

[If large input:]
Note: This is a large input ([N] lines). Will process in chunks with full attention.

Ready to add more inputs or use >>extract to process.
```

---

## Input Types Details

### URL/Web
```bash
# Fetch and save
WebFetch URL → save to 01-INPUTS/[name].md
```

### PDF
```bash
# Extract text, may need human verification
Extract text → save to 01-INPUTS/[name].md
Note any extraction issues
```

### Conversation Export
- Save complete conversation
- Note participants
- Preserve timestamps if available

### Local Files
- Copy to 01-INPUTS/
- Maintain original format
- Note original location in INDEX.md

---

## INDEX.md Template Entry

```markdown
## Input: [Descriptive Name]

- **Source**: /path/to/original/file.md
- **Type**: document
- **Size**: ~500 lines
- **Added**: 2025-01-15
- **Status**: [ ] Not processed
- **Processing Notes**: Contains technical specs for authentication module
- **Summary**: [To be filled after extraction]

### Key Sections
- Section 1: [Brief note]
- Section 2: [Brief note]
```

---

## Related Protocols

- Starting concept → [start-concept.md](start-concept.md)
- Extracting from inputs → [extract.md](extract.md)
- Concept workflow overview → [overview.md](overview.md)
