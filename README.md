# PrestaShop MCP Connector

*[Version française](README.fr.md)*

Connect Claude, ChatGPT or any MCP-compatible assistant to a **PrestaShop** store. Ask questions in plain language — invoices, unpaid orders, customers, sales by region, stock — and let the assistant prepare quotes, without opening the back office.

The connector is a **PrestaShop module**: the MCP server runs inside the store, on the merchant's own hosting. No third-party service, no subscription.

**Try it now with your own Claude**, on a demo store with fictional data: <https://www.studio.sarmate.net/mcp/essai/> (French).
Video demo: <https://youtu.be/KrIiPDKdDL8>

## Tools

Read-only by default.

| Tool | What it does |
|---|---|
| `search_orders` | Orders by reference, customer, status, period, amount, product, or place (city, postcode, French department or region, country) |
| `get_order` | Full order: lines, billing and delivery addresses, status history, payments, invoice |
| `search_invoices` | Invoices by number, period, customer, company, amount, product or billing place, with tax totals |
| `get_invoice` | Invoice detail with VAT breakdown |
| `list_unpaid_orders` | Orders awaiting payment (cheque, bank wire, cash on delivery), with age and contact details, to prepare reminders |
| `search_customers` | Customers by name, company, place, number of orders, amount spent, inactivity, unpaid orders |
| `get_customer` | Customer record: addresses, purchase statistics, recent and unpaid orders |
| `sales_summary` | Revenue and orders by month, product, city, department, region, country or payment method |
| `search_products` | Products with price, stock per combination, sales over 30 and 90 days, estimated stock coverage |
| `report_unsupported_request` | Records a request the connector cannot handle, to improve it |

Optional, only for tokens allowed to write quotes:

| Tool | What it does |
|---|---|
| `create_quote` | Numbered quote with PDF: catalog products (by name, reference or combination) and free lines (services), line or global discounts, shipping. Stored in the module only: no cart, no order, no stock change |
| `get_quote`, `search_quotes`, `cancel_quote` | Read, list and cancel quotes (a cancelled quote keeps its number) |

## Security

- One token per assistant or team, each with its own rights (quotes on or off), per-minute and per-day call limits, and one-click revocation.
- Every call is logged: tool, parameters, result, duration.
- Personal data masking option: first name and initial, truncated e-mail and phone, no street address.
- Quote creation is disabled unless the merchant enables it.
- Tokens are stored hashed.

## Connection

Streamable HTTP endpoint: `https://<your-store>/module/studiomcp/endpoint`

- Claude Code: `claude mcp add --transport http shop https://<your-store>/module/studiomcp/endpoint --header "Authorization: Bearer <token>"`
- claude.ai (Settings → Connectors → Add custom connector): the token can be passed in the URL (`?key=<token>`) when the merchant enables that option, since claude.ai does not send custom headers.

## Compatibility

Tested on PrestaShop 8.2 with claude.ai and Claude Code.

## About

Developed by [Studio Sarmate](https://www.studio.sarmate.net/), which also builds custom PrestaShop modules and MCP servers for other business software. Installation on your store, or a connector for another tool: <https://www.studio.sarmate.net/mcp/>
