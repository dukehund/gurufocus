
## Getting Started

To connect from an MCP-compatible client or your own application:

1. Configure the MCP server URL
2. Add your GuruFocus API key in the `Authorization` header
3. Start making tool calls through the MCP client

Example server endpoint:

```
https://api.gurufocus.com/mcp
```

Example authentication header:

```
Authorization: YOUR_API_KEY
```

#### Claude

These steps work for both **[Claude.ai](http://Claude.ai) (web)** and **Claude Desktop**.

1. Go to **Settings → Connectors**
2. Click **Add custom connector**
3. Enter the server URL: `https://api.gurufocus.com/mcp?authorization=YOUR_API_KEY`
4. Save the connector
5. In any new chat, click **+ → Connectors**
6. Enable **GuruFocus**

#### Claude Code

1. Open your terminal
2. Run:
  ```
  claude mcp add --transport sse gurufocus https://api.gurufocus.com/mcp --header "Authorization: YOUR_API_KEY"
  ```
3. Verify the server:
  ```
  claude mcp list
  ```
4. Start a Claude Code session
5. Use `/mcp` to confirm GuruFocus is available

#### Cursor

1. Open **Cursor Settings**
2. Go to **Tools & MCP**
3. Click **Add new MCP server**
4. Enter:
  - **Name:** `gurufocus`
  - **URL:** `https://api.gurufocus.com/mcp`
5. Add the request header:
  ```
  Authorization: YOUR_API_KEY
  ```
6. Save the server
7. Open a new Agent chat and start using GuruFocus tools

You can also configure GuruFocus in `~/.cursor/mcp.json`:

```
{
  "mcpServers": {
    "gurufocus": {
      "url": "https://mcp.gurufocus.com/api",
      "headers": {
        "Authorization": "YOUR_API_KEY"
      }
    }
  }
}
```

&nbsp;

## Available Tools

Once connected, your AI assistant can use the following GuruFocus MCP tools.

### Stocks by Region

#### `gurufocus_get_stocks_by_region`

Discover stocks by market or geography.

Use this when the user asks for stocks in a region, country group, or market universe.

**Supported region codes**

- `U` = USA
- `E` = Europe
- `A` = Asia
- `C` = Canada
- `B` = UK/Ireland
- `O` = Oceania
- `F` = Africa
- `S` = Latin America
- `I` = India/Pakistan
- `G` = Global

---

### Stock Fundamentals

#### `gurufocus_get_stock_fundamentals`

Get earnings and financial statement data for a stock.

Use this for questions about:

- quarterly data
- TTM revenue
- EPS
- margins
- free cash flow
- balance sheet metrics
- cash flow metrics

### Stock Profile

#### `gurufocus_get_stock_profile`

Get a high-level stock overview.

Use this first for public-company or ticker questions that need an overview, such as:

- company profile
- market cap
- latest earnings date
- profitability
- leverage
- price stats
- high-level valuation context

### Stock Rankings

#### `gurufocus_get_stock_rankings`

Get GuruFocus scoring and valuation-related data.

Use this for questions about:

- GF Score
- GF Value
- valuation vs fair value
- profitability rank
- growth rank
- momentum rank
- balance-sheet rank

### Stock Segments

#### `gurufocus_get_stock_segment`

Get company segment and business mix data.

Use this for questions such as:

- revenue by segment
- operating breakdown
- business-line exposure

### Stock Valuations

#### `gurufocus_get_stock_valuations`

Get historical valuation ratios and valuation context.

Use this for questions about:

- historical P/E
- historical P/S
- historical P/B
- yield-based valuation
- how current valuation compares with past ranges

### Stock Dividends

#### `gurufocus_get_stock_dividends`

Get dividend data for a stock.

Use this for dividend questions about a stock, including:

- dividend amount
- dividend yield
- payout ratio
- ex-dividend date
- payment date
- dividend history

### Stock News

#### `gurufocus_get_stock_news`

Get recent stock-specific news.

Use this for:

- recent company news
- sentiment
- headlines
- analyst-related updates
- notable developments affecting a company or ticker

---

### ETF Data

#### `gurufocus_get_etf_by_symbol`

Get ETF data for a specific symbol.

Use this for ETF questions about a specific symbol, including:

- ETF profile
- holdings-related context
- fund-level metrics

---

### Fund Letters

#### `gurufocus_get_fund_letter_by_quarter`

List fund letters by quarter.

Use this for hedge fund or investor letter questions by quarter, especially when the user asks for:

- recent fund letters
- commentary
- quarterly investor updates

---

### Gurus

#### `gurufocus_get_gurus_list`

Browse available guru profiles.

Use this when the user asks about:

- fund managers
- superinvestors
- guru lists
- browsing available guru profiles

#### `gurufocus_get_guru_by_id`

Get data for a specific guru by ID.

Use this for questions about a specific guru or investor once the guru ID is known, including:

- guru profile
- holdings-related context
- guru-specific data

---

### Insider Activity

#### `gurufocus_get_insiders_by_date`

Get insider trading data for a specific date.

Use this for insider trading questions on a specific date, including:

- insider buying
- insider selling
- notable insider activity

---

## Recommended Tool Selection

When choosing among GuruFocus tools:

- Use `**gurufocus_get_stock_profile**` first for general stock overview questions
- Use `**gurufocus_get_stock_fundamentals**` for earnings, statements, cash flow, and margin questions
- Use `**gurufocus_get_stock_rankings**` for GF Value, GF Score, and rank-based analysis
- Use `**gurufocus_get_stock_valuations**` for valuation-history and multiple-range questions
- Use `**gurufocus_get_stock_dividends**` for dividend questions
- Use `**gurufocus_get_stock_news**` for recent company developments
- Use `**gurufocus_get_stock_segment**` for segment revenue and business mix questions
- Use `**gurufocus_get_etf_by_symbol**` for ETF-specific questions
- Use `**gurufocus_get_gurus_list**` to browse gurus
- Use `**gurufocus_get_guru_by_id**` when the guru ID is already known
- Use `**gurufocus_get_fund_letter_by_quarter**` for investor letters by quarter
- Use `**gurufocus_get_insiders_by_date**` for insider activity on a specific date
- Use `**gurufocus_get_stocks_by_region**` for stock universes by region

---

## Example Usage

After connecting, users can ask questions like:

- “Show me Apple’s company profile and latest valuation context”
- “What is Johnson & Johnson’s dividend yield and payout ratio?”
- “Compare Microsoft’s GF Value and GF Score”
- “Show Tesla’s latest stock news”
- “What were Nvidia’s recent revenue and EPS trends?”
- “Break down Amazon’s revenue by segment”
- “Show Meta’s historical valuation ranges”
- “List available premium gurus”
- “Show me Warren Buffett’s guru profile”
- “Find fund letters for 2024Q1”
- “What insider activity happened on 2023-10-01?”
- “Show ETF data for SPY”

---

## Notes

- Tool availability may depend on the user’s GuruFocus subscription plan
- Some data fields may vary by region, market, and security type
- Historical depth may vary by dataset

&nbsp;
