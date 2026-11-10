# MakerLens

**See your real Etsy profit after every fee, plus a transparent cash-flow forecast.**

Etsy shows sellers their sales, but not what they actually keep. MakerLens reads the CSV files Etsy lets sellers download and shows:

- **Real profit** after transaction, processing, listing, ad and shipping-label fees, refunds and material costs
- **Profit per product**, with products that lose money flagged
- **Profit by month**
- **A 3/6/12-month cash-flow forecast** with seasonal detection, a best/worst-case range, and a plain-English explanation of how every number is calculated

🔒 **Privacy first:** everything runs in the browser. No server, no sign-up, and seller data never leaves their computer.

## Try it
Open `index.html` and click **Try with sample data** (a fictional 12-month candle shop).

## How it works
| Step | What happens |
|---|---|
| 1. Parse | A small CSV parser reads Etsy's monthly statements (Date, Type, Title, Info, Currency, Amount, Fees & Taxes, Net) and the optional Order Items export. File types are detected automatically. |
| 2. Classify | Each statement row is grouped by type: sales, refunds, and fee categories. Bank deposits are excluded because they're transfers, not profit. |
| 3. Profit | Real profit = Etsy payout (sales + fees + refunds) − material costs entered by the seller. |
| 4. Per product | Fees and refunds are allocated to products by share of sales, since Etsy doesn't itemise every fee. |
| 5. Forecast | Base = average of the last 6 months with seasonality removed. Seasonal factor per month = that month's sales ÷ average (needs 12 months), or seller-selected busy months. Range = ±10% + 2.5% per month ahead. |

## Tech
Plain HTML, CSS and JavaScript in a single file. No libraries, no build step. Charts are hand-made SVG. Hosted on GitHub Pages.

## Roadmap
- Guided step-by-step download instructions with screenshots
- Support for more export formats and currencies in one file
- Exportable report (PDF)
- Feedback-driven features from real sellers

## About
Built by Bruno, a Computer Science & Business Administration student at Northeastern University (London Scholars).
Not affiliated with Etsy. Figures are for guidance only, not financial or tax advice.
