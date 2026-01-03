---
description: Manage project templates for documents and code
allowed-tools:
  - Read
  - Write
  - Bash
  - WebFetch
  - Glob
---

# Template - Project Template Management

Manage and use templates for documents, code, and project structures.

## Usage

```bash
# List available templates
/template list

# Get/download a template
/template get govdoc-external
/template get govdoc-memo

# Create file from template
/template create memo "ขอความอนุเคราะห์"

# Show template info
/template info govdoc-external
```

## Built-in Templates

### Thai Government Documents (หนังสือราชการ)

| Template | Description | File |
|----------|-------------|------|
| `govdoc-external` | หนังสือภายนอก (External letter) | .ccc/templates/govdoc/external.md |
| `govdoc-internal` | หนังสือภายใน (Internal letter) | .ccc/templates/govdoc/internal.md |
| `govdoc-memo` | บันทึกข้อความ (Memo) | .ccc/templates/govdoc/memo.md |
| `govdoc-order` | คำสั่ง (Order) | .ccc/templates/govdoc/order.md |
| `govdoc-announce` | ประกาศ (Announcement) | .ccc/templates/govdoc/announce.md |

### Project Templates

| Template | Description |
|----------|-------------|
| `spec` | Specification document |
| `plan` | Implementation plan |
| `retro` | Retrospective |

## Commands

### /template list

Show all available templates:

```
📁 Available Templates

Thai Government Documents (หนังสือราชการ):
  govdoc-external   หนังสือภายนอก
  govdoc-internal   หนังสือภายใน
  govdoc-memo       บันทึกข้อความ
  govdoc-order      คำสั่ง
  govdoc-announce   ประกาศ

Project Templates:
  spec              Specification document
  plan              Implementation plan
  retro             Retrospective

Use: /template get <name>
```

### /template get <name>

Download/create template in `.ccc/templates/`:

```bash
/template get govdoc-external
```

**Output:**
```
✅ Template created: .ccc/templates/govdoc/external.md

Use: /template create govdoc-external "Your title"
```

### /template create <name> "title"

Generate document from template:

```bash
/template create govdoc-memo "ขอความอนุเคราะห์ข้อมูล"
```

**Output:**
```
✅ Document created: .ccc/docs/memo-2024-01-15-001.md

Edit the document, then use MCP to convert to Word/PDF.
```

## Template Format

Templates use markdown with placeholders:

```markdown
# {{DOCUMENT_TYPE}}: {{TITLE}}

**เลขที่**: {{DOCUMENT_NUMBER}}
**วันที่**: {{DATE}}
**ถึง**: {{RECIPIENT}}
**จาก**: {{SENDER}}

## เรื่อง
{{SUBJECT}}

## รายละเอียด
{{CONTENT}}

## ลงชื่อ
{{SIGNATURE}}
{{POSITION}}
```

## Thai Government Document Templates

### หนังสือภายนอก (External Letter)

```markdown
# หนังสือภายนอก

**ที่**: {{ORG_CODE}}/{{YEAR}}
**ส่วนราชการ**: {{DEPARTMENT}}

**วันที่**: {{DATE}}

**เรื่อง**: {{SUBJECT}}

**เรียน**: {{RECIPIENT}}

**สิ่งที่ส่งมาด้วย**: {{ATTACHMENTS}}

{{CONTENT}}

จึงเรียนมาเพื่อโปรด{{ACTION}}

ขอแสดงความนับถือ

{{SIGNATURE}}
({{NAME}})
{{POSITION}}

{{DEPARTMENT}}
โทร. {{PHONE}}
```

### บันทึกข้อความ (Memo)

```markdown
# บันทึกข้อความ

**ส่วนราชการ**: {{DEPARTMENT}}
**ที่**: {{DOC_NUMBER}}
**วันที่**: {{DATE}}

**เรื่อง**: {{SUBJECT}}

**เรียน**: {{RECIPIENT}}

{{CONTENT}}

จึงเรียนมาเพื่อโปรด{{ACTION}}

{{SIGNATURE}}
({{NAME}})
{{POSITION}}
```

## Integration with MCP

After creating document from template, use MCP to convert:

```bash
# If document-operations MCP is installed
# Claude can convert markdown to Word/PDF
```

## Directory Structure

```
.ccc/
├── templates/
│   ├── govdoc/
│   │   ├── external.md
│   │   ├── internal.md
│   │   ├── memo.md
│   │   ├── order.md
│   │   └── announce.md
│   └── project/
│       ├── spec.md
│       ├── plan.md
│       └── retro.md
└── docs/                  ← Generated documents
    ├── memo-2024-01-15-001.md
    └── external-2024-01-15-001.md
```

## Examples

### Create a Memo

```bash
/template create govdoc-memo "ขอความอนุเคราะห์ข้อมูลสถิติ"
```

### Create External Letter

```bash
/template create govdoc-external "ขอเชิญเป็นวิทยากร"
```

### List and Get Templates

```bash
/template list
/template get govdoc-external
/template info govdoc-external
```
