# MakerLens

**See what you really keep from every Etsy sale.**

🔗 **Live:** https://bruno-240608.github.io/makerlens/

Etsy shows sellers what they sold, but not what's left after all the fees. MakerLens reads the CSV files Etsy already lets sellers download and shows:

- **Real profit** after Etsy's fees (transaction, payment processing, listing, ads, shipping labels, tax on fees), refunds and the seller's own material costs
- **Profit per product**, with a summary line naming the products that lose money
- **Price tools:** a price slider that shows how much room a new price gives you (it never guesses how customers will react; the seller can enter their own guess), and a planner for new products
- **A 3/6/12-month forecast** with a likely range, busy-season detection, an option to base it on recent months or the same months last year, and a plain-words income statement ("your next months at a glance")

## Privacy you can check

Everything runs in the seller's own browser. There's no server, no account, no database and no AI. The Etsy files never leave the seller's computer.

I didn't want this to be just a claim, so the site lets people verify it:
- **The Wi-Fi test:** turn off your internet and upload your files. It still works, and the page confirms "You're offline, and it still worked."
- **What's saved:** the privacy section lists exactly what's stored in the browser (only product costs and currency choice) and lets you clear it.
- **The code is public:** this repo.

The only things that touch the internet are a cookie-free visit counter (GoatCounter) and an optional feedback form.

## How it works

| Step | What happens |
|---|---|
| 1. Read | A hand-written CSV parser reads Etsy's monthly statements and Order Items exports (quotes, commas inside fields, BOM, `--` values). It works out which file is which and explains wrong or incomplete files in plain words. |
| 2. Sort | Each statement row is sorted into sales, fees (by Type and Title), refunds and tax. Bank deposits and card payments to Etsy are left out because they move money, they aren't profit. Sales tax paid by the buyer comes off sales instead of counting as a fee. |
| 3. Per product | Order Items lines are grouped by order. Order-level discounts are spread over the items. Each fee is matched to its order number and split by item value; shop-wide costs (like Etsy Ads) are shared by sales. Costs for orders that aren't in the Order Items file are kept out of the table and explained. If the statement and orders use different currencies, each order is converted at the rate Etsy actually used. |
| 4. Honesty checks | Until material costs are entered, profit is labelled "before your costs" and no product gets a green tick. Estimates say they're estimates, with "How is this worked out?" explanations. |
| 5. Forecast | Base = recent average with seasonality removed; seasonal factors from 12+ months of data or months the seller picks; range widens the further ahead it goes. |

## Testing

- Tested on **real Etsy exports** from two shops found in public repositories (10 months of statements from a small shop, and a month of statements + Order Items from a larger shop in two currencies). This found and fixed 7 bugs, including discounts being ignored and mixed currencies. Total profit matches an independent calculation to the cent.
- **User testing** with a fresh-eyes tester acting as a non-technical seller, which led to the trust fixes above, plainer wording and a phone layout.

## Tech

Plain HTML, CSS and JavaScript in one file. No libraries, no build step, hand-made SVG charts. Hosted on GitHub Pages. Tested with Playwright.

## About

Built by Bruno, a Computer Science & Business Administration student at Northeastern University (London). I decided what to build and how it should behave, tested it with users and real data, and built it with AI-assisted development (Claude).

Not affiliated with Etsy. Figures are for guidance only, not financial or tax advice.
