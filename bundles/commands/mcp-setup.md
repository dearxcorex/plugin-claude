---
description: Setup MCP servers for enhanced capabilities
allowed-tools:
  - Read
  - Write
  - Bash
  - WebFetch
---

# MCP Setup - Model Context Protocol Server Configuration

Setup MCP (Model Context Protocol) servers to extend Claude Code capabilities.

## Usage

```bash
# Show available MCP servers
/mcp-setup

# Setup document processing servers
/mcp-setup documents

# Setup specific server
/mcp-setup word
/mcp-setup pdf
```

## What is MCP?

Model Context Protocol (MCP) is an open protocol that enables Claude to interact with external tools and services. MCP servers add capabilities like:

- Document processing (Word, PDF, Excel)
- Database access
- API integrations
- File system operations

## Available MCP Server Guides

### Document Processing

| Server | Capabilities | Install |
|--------|--------------|---------|
| document-operations | Word, Excel, PDF | `uvx document-operations-mcp` |
| Office-Word-MCP | Word documents | `npx @anthropic/office-word-mcp` |
| docx-processor | DOCX files | `npx docx-processor-mcp` |

### Development Tools

| Server | Capabilities | Install |
|--------|--------------|---------|
| filesystem | File operations | Built-in |
| git | Git operations | `npx @anthropic/git-mcp` |
| github | GitHub API | `npx @anthropic/github-mcp` |

## Setup Guide

### /mcp-setup documents

Setup document processing MCP servers:

**Step 1: Check Requirements**
```bash
# Check Python (for uvx)
python --version  # Need 3.10+

# Check Node.js (for npx)
node --version    # Need 18+
```

**Step 2: Install uv (if needed)**
```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Step 3: Add to Claude Settings**

Edit `~/.claude/settings.json`:

```json
{
  "mcpServers": {
    "document-operations": {
      "command": "uvx",
      "args": ["document-operations-mcp"],
      "env": {}
    }
  }
}
```

**Step 4: Restart Claude Code**
```bash
# Exit and restart
exit
claude
```

**Step 5: Verify**
```bash
/mcp
# Should show document-operations server
```

### /mcp-setup word

Setup Word document processing:

```json
{
  "mcpServers": {
    "word": {
      "command": "npx",
      "args": ["-y", "@anthropic/office-word-mcp"],
      "env": {}
    }
  }
}
```

**Capabilities:**
- Create Word documents
- Read/edit existing .docx
- Add text, tables, images
- Format content
- Save to .docx

### /mcp-setup pdf

Setup PDF processing:

```json
{
  "mcpServers": {
    "pdf": {
      "command": "uvx",
      "args": ["pdf-operations-mcp"],
      "env": {}
    }
  }
}
```

**Capabilities:**
- Read PDF content
- Extract text
- Convert to/from PDF

## Full Document Setup

For complete document processing, add all servers:

```json
{
  "mcpServers": {
    "document-operations": {
      "command": "uvx",
      "args": ["document-operations-mcp"]
    },
    "word": {
      "command": "npx",
      "args": ["-y", "office-word-mcp-server"]
    }
  }
}
```

## Workflow with MCP

### Creating Thai Government Documents

```bash
# 1. Generate document from template
/template create govdoc-memo "ขอความอนุเคราะห์"

# 2. Document agent creates .md file
# → .ccc/docs/memo-2024-01-15-001.md

# 3. With MCP, Claude can convert to Word
# "Convert this memo to Word format"
# → Creates .docx with proper formatting

# 4. Print or share the .docx file
```

### Document Conversion Flow

```
Markdown (.md)
     ↓
Template + Content
     ↓
Document Agent
     ↓
.ccc/docs/document.md
     ↓
MCP (document-operations)
     ↓
Word/PDF Output
```

## Troubleshooting

### "MCP server not found"
```bash
# Check if server is installed
uvx document-operations-mcp --help

# Reinstall
uv pip install document-operations-mcp
```

### "Command not found: uvx"
```bash
# Install uv first
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc  # or restart terminal
```

### "Settings not applied"
```bash
# Restart Claude Code completely
exit
claude
/mcp  # Check servers
```

## MCP Resources

- [MCP Specification](https://modelcontextprotocol.io/specification)
- [Document Operations MCP](https://www.pulsemcp.com/servers/alejandroballesteros-document-operations)
- [Office Word MCP](https://github.com/GongRzhe/Office-Word-MCP-Server)

## Output

### /mcp-setup
```
📦 MCP Setup Guide

Available configurations:
  documents  - Word, Excel, PDF processing
  word       - Microsoft Word only
  pdf        - PDF processing only

Current MCP status:
  Run /mcp to see configured servers

Quick setup:
  1. Edit ~/.claude/settings.json
  2. Add server configuration
  3. Restart Claude Code
  4. Verify with /mcp

Use: /mcp-setup <type> for detailed guide
```

### /mcp-setup documents
```
📄 Document Processing MCP Setup

Step 1: Install dependencies
  curl -LsSf https://astral.sh/uv/install.sh | sh

Step 2: Add to ~/.claude/settings.json:
  {
    "mcpServers": {
      "document-operations": {
        "command": "uvx",
        "args": ["document-operations-mcp"]
      }
    }
  }

Step 3: Restart Claude Code
  exit
  claude

Step 4: Verify
  /mcp

After setup, you can:
  - Convert markdown to Word/PDF
  - Read and edit existing documents
  - Create formatted Thai government documents
```
