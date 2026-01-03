---
description: Create and manage your own project templates
allowed-tools:
  - Read
  - Write
  - Bash
  - WebFetch
  - Glob
---

# Template - Create Your Own Templates

Create, manage, and use your own custom templates for documents, code, or any project files.

## Usage

```bash
# Create a new template
/template new <name>

# List your templates
/template list

# Edit a template
/template edit <name>

# Use template to generate
/template use <name> "Title"

# Import from URL or file
/template import <source>

# Delete a template
/template delete <name>
```

## Creating Templates

### /template new <name>

Create a new blank template:

```bash
/template new memo
/template new report
/template new govdoc-external
```

**What happens:**
1. Creates `.ccc/templates/<name>.md`
2. Opens for editing
3. You define the structure

**Example - Creating a memo template:**

```bash
/template new memo
```

Then you write your template:

```markdown
# บันทึกข้อความ

**ส่วนราชการ**: {{DEPARTMENT}}
**ที่**: {{DOC_NUMBER}}
**วันที่**: {{DATE}}

**เรื่อง**: {{SUBJECT}}

**เรียน**: {{RECIPIENT}}

{{CONTENT}}

จึงเรียนมาเพื่อโปรด{{ACTION}}

({{SIGNATURE}})
{{NAME}}
{{POSITION}}
```

### /template edit <name>

Edit an existing template:

```bash
/template edit memo
```

Opens `.ccc/templates/memo.md` for editing.

## Template Syntax

### Placeholders

Use `{{NAME}}` for dynamic content:

```markdown
# {{TITLE}}

**Date**: {{DATE}}
**Author**: {{AUTHOR}}

## Content
{{BODY}}
```

### Common Placeholders

| Placeholder | Use For |
|-------------|---------|
| `{{TITLE}}` | Document title |
| `{{DATE}}` | Current date |
| `{{AUTHOR}}` | Author name |
| `{{CONTENT}}` | Main content |
| `{{SUBJECT}}` | Subject line |
| `{{RECIPIENT}}` | Recipient |
| `{{SIGNATURE}}` | Signature |

### Custom Placeholders

Create any placeholder you need:

```markdown
{{DEPARTMENT}}
{{DOC_NUMBER}}
{{PHONE}}
{{EMAIL}}
{{CUSTOM_FIELD}}
```

## Using Templates

### /template use <name> "Title"

Generate document from your template:

```bash
/template use memo "ขอความอนุเคราะห์ข้อมูล"
```

**What happens:**
1. Reads `.ccc/templates/memo.md`
2. Claude fills placeholders based on title and context
3. Creates `.ccc/docs/memo-YYYY-MM-DD-XXX.md`
4. You review and finalize

## Importing Templates

### /template import <source>

Import from URL:
```bash
/template import https://raw.githubusercontent.com/user/repo/template.md
```

Import from local file:
```bash
/template import ./downloads/template.md
```

Import from another project:
```bash
/template import /path/to/project/.ccc/templates/memo.md
```

## Managing Templates

### /template list

Show all your templates:

```
📁 Your Templates (.ccc/templates/)

  memo.md              - Created 2024-01-15
  external-letter.md   - Created 2024-01-14
  report.md            - Created 2024-01-10

Total: 3 templates
```

### /template delete <name>

Remove a template:

```bash
/template delete old-template
```

## Directory Structure

```
.ccc/
├── templates/           ← Your templates
│   ├── memo.md
│   ├── external-letter.md
│   └── report.md
└── docs/                ← Generated documents
    ├── memo-2024-01-15-001.md
    └── report-2024-01-15-001.md
```

## Example: Thai Government Memo

### Step 1: Create template

```bash
/template new govdoc-memo
```

### Step 2: Write your template

```markdown
# บันทึกข้อความ

**ส่วนราชการ**: {{DEPARTMENT}}
**ที่**: {{DOC_NUMBER}}
**วันที่**: {{DATE}}

---

**เรื่อง**: {{SUBJECT}}

**เรียน**: {{RECIPIENT}}

{{CONTENT}}

จึงเรียนมาเพื่อโปรด{{ACTION}}

---

{{SIGNATURE}}
({{NAME}})
{{POSITION}}
```

### Step 3: Use it

```bash
/template use govdoc-memo "ขอความอนุเคราะห์"
```

### Step 4: Claude generates

Creates `.ccc/docs/govdoc-memo-2024-01-15-001.md` with placeholders filled.

## Tips

### Do
- Create templates for documents you use often
- Use clear placeholder names
- Keep templates in version control

### Don't
- Hardcode values that change
- Make templates too complex
- Forget to test templates

## Quick Reference

| Command | Action |
|---------|--------|
| `/template new <name>` | Create template |
| `/template list` | Show templates |
| `/template edit <name>` | Edit template |
| `/template use <name> "title"` | Generate from template |
| `/template import <url>` | Import template |
| `/template delete <name>` | Delete template |
