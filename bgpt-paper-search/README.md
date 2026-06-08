# BGPT Paper Search

Search scientific papers and retrieve structured experimental data extracted from full-text studies via the BGPT MCP server.

## What It Does

Unlike traditional literature databases that return titles and abstracts, BGPT returns structured data from the actual paper content — methods, quantitative results, sample sizes, quality assessments, and 25+ metadata fields per paper.

## Setup

BGPT is a remote MCP server — no local installation required.

### Claude Desktop / Claude Code

Add to your MCP configuration:

```json
{
  "mcpServers": {
    "bgpt": {
      "command": "npx",
      "args": ["mcp-remote", "https://bgpt.pro/mcp/sse"]
    }
  }
}
```

### Alternative

```bash
npx bgpt-mcp
```

## Usage

```
/bgpt-paper-search
```

Example query:
```
Search for papers about: "CRISPR gene editing efficiency in human cells"
```

## What You Get Back

Each result includes:
- Title, authors, journal, year, DOI
- **Methods**: Experimental techniques, models, protocols
- **Results**: Key findings with quantitative data
- **Sample sizes**: Number of subjects/samples
- **Quality scores**: Study quality assessments
- **Conclusions**: Author conclusions and implications

## Use Cases

- Systematic or scoping literature reviews
- Finding quantitative results and effect sizes across studies
- Comparing methodologies between studies
- Building evidence tables for meta-analyses
- Accessing structured full-text data (not just abstracts)

## Pricing

| Tier | Details |
|------|---------|
| Free | 50 searches per network, no API key |
| Paid | $0.01 per result with API key from [bgpt.pro/mcp](https://bgpt.pro/mcp) |

## Credits

- Skill author: BGPT
- Website: https://bgpt.pro/mcp
- GitHub: https://github.com/connerlambden/bgpt-mcp

## License

MIT
