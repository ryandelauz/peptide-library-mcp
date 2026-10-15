# Claude

**claude.ai / Claude Desktop:** Customize → Connectors → Add custom connector. Name: `Peptide Library`. URL: `https://peptidelibrary.app/mcp`. No authentication. Team and Enterprise: an owner adds it under Organization settings → Connectors.

**Claude Code:**

```bash
claude mcp add --transport http peptide-library https://peptidelibrary.app/mcp
```

Try: "Using Peptide Library, summarize the evidence for BPC-157 by study type and link the sources."
