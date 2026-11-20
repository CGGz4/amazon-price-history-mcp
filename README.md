# Amazon Price Tracker MCP Server – AIPriceHistory

**Free Amazon Price History MCP Server for Claude Code, Cursor, and AI Assistants.**

Connect your AI assistant to historical Amazon product prices using the **Model Context Protocol (MCP)**. Check Amazon price history, lowest and highest recorded prices, average prices, and historical price changes across **23 Amazon marketplaces worldwide**.

[![MCP](https://img.shields.io/badge/MCP-Streamable_HTTP-blue)](https://modelcontextprotocol.io/)
[![Amazon](https://img.shields.io/badge/Amazon-23_Marketplaces-orange)](https://aipricehistory.com/)
[![Free](https://img.shields.io/badge/Free-100_Products%2FWeek-brightgreen)](https://aipricehistory.com/)

**Website:** https://aipricehistory.com/

**MCP Endpoint:** `https://aipricehistory.com/api/mcp`

## Features

- **Amazon Price History:** Retrieve historical prices for Amazon products using their ASIN.
- **Lowest Price Checker:** Find the lowest recorded Amazon price and its date.
- **Highest Price Checker:** Identify the highest historical price and its date.
- **Average Price Analysis:** Compare current prices with historical averages.
- **Price Trend Analysis:** Examine dated price changes over selected periods.
- **Global Amazon Support:** Track prices across 23 Amazon marketplaces, including the US, UK, India, Australia, Canada, Germany, and Japan.
- **AI Assistant Integration:** Compatible with Claude Code, Cursor, and MCP clients supporting remote HTTP servers with custom headers.
- **Free MCP API Access:** Analyze 100 unique Amazon products every week.

## Quick Start

### 1. Get Your Free API Key

1. Visit [AIPriceHistory](https://aipricehistory.com/).
2. Create a free account or sign in.
3. Generate an MCP access key from the MCP panel.
4. Copy your access key and store it securely.

### 2. Install in Claude Code

Run:

```bash
claude mcp add --transport http aipricehistory https://aipricehistory.com/api/mcp --header "Authorization: Bearer YOUR_KEY"
```

Replace `YOUR_KEY` with your API key.

### 3. Configure Cursor or Other MCP Clients

For clients supporting JSON-based MCP configuration:

```json
{
  "mcpServers": {
    "aipricehistory": {
      "url": "https://aipricehistory.com/api/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_KEY"
      }
    }
  }
}
```

**Transport:** Streamable HTTP

**Authentication:** Bearer Token

**Response Format:** JSON

## Available MCP Tools

### `get_price_history`

Retrieve the price history of an Amazon product.

**Parameters**

| Parameter | Required | Description |
|---|---|---|
| `asin` | Yes | 10-character Amazon product ASIN |
| `marketplace` | No | Amazon marketplace domain or country code. Default: `amazon.in` |
| `days` | No | Retrieve price history for the last N days |

**Returns:**

- Product title and currency
- Current recorded price
- Lowest recorded price and date
- Highest recorded price and date
- Average historical price
- Difference from historical lowest price
- Number of recorded price checks
- Dated price changes
- AIPriceHistory product URL

**Example AI prompt:**

> Check the Amazon price history for ASIN B0CX23V2ZK on amazon.in over the last 90 days. Compare the current price with its historical lowest and average prices. Is it a good deal?

### `get_usage`

Check your free weekly Amazon price history allowance.

**Returns:**

- Weekly product lookup limit
- Unique products queried
- Remaining free lookups
- Weekly reset information

**Example AI prompt:**

> How many Amazon price history lookups do I have left this week?

## Supported Amazon Marketplaces

AIPriceHistory supports Amazon price tracking across **23 marketplaces**.

| Region | Supported Amazon Stores |
|---|---|
| North & South America | `amazon.com`, `amazon.ca`, `amazon.com.mx`, `amazon.com.br` |
| Europe | `amazon.co.uk`, `amazon.de`, `amazon.fr`, `amazon.it`, `amazon.es`, `amazon.nl`, `amazon.com.be`, `amazon.ie`, `amazon.pl`, `amazon.se`, `amazon.com.tr` |
| Middle East & Africa | `amazon.ae`, `amazon.sa`, `amazon.eg` |
| Asia-Pacific | `amazon.in`, `amazon.co.jp`, `amazon.com.au`, `amazon.sg` |

Specify the marketplace using its Amazon domain or supported country code, such as `us`, `in`, `uk`, or `au`.

## Free Usage Limits

| Feature | Free Allowance |
|---|---|
| Unique products per week | 100 |
| API requests per minute | 60 |
| Supported marketplaces | 23 |
| Repeated lookups | Free within the same week |
| Untracked products | Not counted |
| Weekly reset | Monday, India Standard Time |
| Cost | Free |

**How product counting works**

One unique product means one ASIN on one Amazon marketplace.

For example:

- `B0CX23V2ZK` on `amazon.in` counts as one product.
- The same ASIN on `amazon.com` counts as another product.
- Repeating a query for the same product and marketplace during the same week does not consume another unique-product allowance.

## Example Use Cases

### Amazon Lowest Price Finder

> What is the lowest recorded price for ASIN B0CX23V2ZK on Amazon India?

### Amazon Price Drop Analysis

> Analyze the price history of ASIN B0CX23V2ZK over the last 90 days. How much has the price changed?

### Amazon Deal Evaluation

> Is the current price of ASIN B0CX23V2ZK on Amazon a good deal compared with its historical prices?

### Amazon Historical Price Comparison

> Compare the current price, lowest price, highest price, and average price for ASIN B0CX23V2ZK.

## How It Works

1. Your AI assistant calls the `get_price_history` MCP tool with an Amazon ASIN.
2. AIPriceHistory retrieves available historical pricing records for the requested marketplace.
3. The MCP server returns structured JSON pricing data.
4. Your AI assistant uses the data to analyze historical prices and answer your question.

**Data limitations:**

- Prices are recorded approximately once per day.
- Historical prices represent the listed Amazon store price at the time of each check.
- Coupons, bank offers, and delivery charges are excluded.
- Only products already tracked by AIPriceHistory have historical data.
- The server provides historical data, not future price predictions.

If a product is not tracked, submit its Amazon URL on [AIPriceHistory](https://aipricehistory.com/) to begin building its price history.

## Frequently Asked Questions

### Is this Amazon Price Tracker MCP Server free?

Yes. Registered users can retrieve price history for 100 unique Amazon products per week for free.

### Can I use this MCP server with Claude Code?

Yes. Claude Code supports remote MCP servers using Streamable HTTP and custom authorization headers.

### Does it work with Cursor?

Yes. Configure the remote MCP endpoint and Bearer authorization header in your Cursor MCP settings.

### Does it support Amazon USA and Amazon India?

Yes. The server supports Amazon USA, India, UK, Australia, Canada, Germany, Japan, UAE, Saudi Arabia, and other supported marketplaces.

### Can it predict Amazon price drops?

No. It provides historical Amazon pricing data to help evaluate current prices. It does not predict future price movements.

### Is this an official Amazon API?

No. AIPriceHistory is an independent Amazon price tracking service and is not affiliated with or endorsed by Amazon.

### Is an API key required?

Yes. Create a free AIPriceHistory account and generate an MCP access key. Keep your key private and never commit it to a public GitHub repository.

## Security

- MCP access keys are displayed only once.
- AIPriceHistory stores a hash of each key.
- You can replace a compromised key.
- Generating a new key immediately invalidates the previous key.
- Never publish your API key in source code, screenshots, or GitHub commits.

## Get Started

Use **AIPriceHistory MCP Server** to access Amazon price history directly from your AI assistant.

**[Get Your Free MCP Access Key](https://aipricehistory.com/)**

**MCP Endpoint:** `https://aipricehistory.com/api/mcp`

Free Amazon price history for up to **100 unique products per week** across 23 marketplaces.

---

**Keywords:** Amazon Price Tracker MCP, Amazon Price History MCP Server, Amazon MCP Server, Amazon Price History API, Amazon Lowest Price Checker, Amazon Price Tracker for Claude Code, Cursor Amazon MCP, Model Context Protocol, Amazon Price Analysis, AI Shopping Assistant.

**Powered by [AIPriceHistory](https://aipricehistory.com/)**
