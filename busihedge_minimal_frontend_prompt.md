# BusiHedge Frontend Demo — Google Stitch Prompt

Build a single-page static website (HTML/CSS/JS, no frameworks) for a fuel hedging platform called BusiHedge. This is a demo/concept site, not a production app. All data is hardcoded — no APIs.

## Design philosophy

Look at how Stripe, Linear, and Ramp design their product pages — restrained, typographic, lots of breathing room. Avoid anything that looks like a Bootstrap template or AI-generated landing page. No gradients on buttons, no excessive rounded corners, no generic hero sections, no stock illustrations, no emoji, no "Get Started Free" CTAs.

Specific rules:
- One typeface only: Inter (import from Google Fonts). Use weight to create hierarchy, not size variation.
- Background: #fafafa off-white. Cards: #ffffff with a 1px #e5e5e5 border. No shadows.
- Text: #111 primary, #666 secondary, #999 tertiary.
- One accent color only: #0066ff for interactive elements and selected states.
- Green #16a34a for payouts/savings. Red #dc2626 for risk/cost. Use sparingly — only on numbers, never on backgrounds.
- Monospaced font (JetBrains Mono or SF Mono from Google Fonts) for all dollar amounts and percentages.
- No icons except where absolutely necessary. If you must, use simple inline SVG — no icon libraries.
- Minimal borders. Use whitespace to separate sections, not lines.
- Everything should feel like a Bloomberg terminal had a baby with a clean fintech app.

## Site structure

One HTML page with three views controlled by simple JS tab switching (no routing library). The three views are: Markets, Contract Detail, and My Contracts. Default view is Markets.

Top navigation bar: fixed, white background, bottom border 1px #e5e5e5.
- Left: "BusiHedge" in bold Inter 600 weight, no logo.
- Center: three text links as tabs — "Markets" "My Contracts" "Portfolio" — the active one has a 2px bottom border in accent blue.
- Right: "Atlanta, GA" as a small location label and a circle with initials "AF" as avatar placeholder.

---

### View 1: Markets

A clean list of available hedging contracts. No card grid — use a table-like list layout, one row per market, full-width.

At the top, a single line with filter pills (small, outlined, not filled): "All" "Diesel" "Gasoline" — and on the right side a small region dropdown: "Atlanta"

Below that, the markets list. Each row is separated by a thin 1px bottom border. Each row contains:

**Row layout (single line per market):**
Left side:
- Market name in medium weight: "Atlanta Diesel"
- Duration tag in small light text: "Week of Mar 31" or "April Monthly"

Center section — a set of 5-6 inline strike prices displayed as a compact horizontal strip:

$4.80   $5.00   $5.10   $5.20   $5.40
 28¢     18¢     12¢      7¢      2¢

The strikes are in regular weight. Below each strike in small secondary text is the hedge cost per gallon. The strike nearest to the current price should have a subtle blue background pill to indicate "at the money."

Right side:
- Current reference price in monospace: "$5.09"
- Small trend indicator: "+$0.34" in red text (or green if price dropped)
- A small right arrow "→" that indicates clickable

The whole row is clickable and navigates to the Contract Detail view.

Show 5-6 market rows:
1. Atlanta Diesel — Week of Mar 31 (current ref $5.09, strikes at 4.80/5.00/5.10/5.20/5.40)
2. Atlanta Diesel — Week of Apr 7 (slightly higher costs)
3. Atlanta Diesel — April Monthly ($5.12 ref, wider cost range)
4. Atlanta Gasoline — Week of Mar 31 ($3.79 ref)
5. Southeast Diesel — Week of Mar 31 ($5.04 ref)

---

### View 2: Contract Detail

Shown when clicking into a specific market row. Has a small "← Back to Markets" text link at top left.

**Header section:**
- Market title: "Atlanta Diesel — Week of Mar 31, 2026"
- Below in secondary text: "Settlement: EIA PADD 1C weekly retail diesel price, published Apr 1"
- Status in small text: "Open · Closes Mar 30, 11:59 PM ET"

**Two-column layout below:**

**Left column (55%):**

A simple price chart. Draw this with inline SVG or vanilla canvas — no Chart.js or D3. Show a simplified line chart of diesel price over the last 8 weeks trending upward from ~$3.75 to ~$5.09. Add a light blue shaded band around the line for the last 2 weeks representing the P10-P90 forecast range. Draw a horizontal dashed line across the chart at the selected strike price, with a small label on the right edge showing the strike value.

Below the chart, the **strike ladder** as a clean table:

| Strike        | Probability | Hedge Cost | Coverage Vol |
|--------------|-------------|------------|-------------|
| Above $5.40  | 12%         | 2¢/gal     | 8.2k gal    |
| Above $5.20  | 28%         | 7¢/gal     | 14.5k gal   |
| Above $5.10  | 41%         | 12¢/gal    | 22.1k gal   |
| Above $5.00  | 58%         | 18¢/gal    | 31.4k gal   |
| Above $4.80  | 79%         | 28¢/gal    | 12.8k gal   |

Table styling: no visible header background, thin bottom borders only, left-aligned text. The selected row has a very subtle blue left border (3px) and slightly tinted background. Clicking a row updates the selected strike in the order panel.

**Right column (45%):**

The order panel. White card with border.

Section label in small caps or uppercase letterspacing: "HEDGE ORDER"

Form fields with minimal styling (just a bottom border, no box):
- "Strike price" — dropdown showing the selected strike, e.g. "$5.10 / gal"
- "Weekly volume" — number input, default 2000, with "gallons" label
- "Duration" — three small toggle pills: "1 wk" "2 wk" "4 wk"

Below the form, a summary section with a light gray background (#f5f5f5):

"If Atlanta diesel exceeds $5.10/gal:"
Premium          $240.00
                 (12¢ × 2,000 gal)
Max downside     $240.00 (premium only)
Settlement       Apr 1, automatic

All dollar amounts in monospace. Labels in secondary text, values in primary bold.

Primary button: "Get Quote — $240" — solid #0066ff background, white text, no rounded corners (2px max border radius).

Below in tertiary text: "Quote valid 15 min · Settlement on EIA published price"

Below the order panel, a minimal three-step explainer:

1 Choose a strike price above which you want protection
2 Pay a fixed premium — that's your maximum cost
3 If the published price exceeds your strike, you're paid automatically

Numbers "1 2 3" in accent blue, text in secondary gray. No boxes, no icons, just clean type.

---

### View 3: My Contracts

Simple table of user's contracts.

Summary bar at top — four numbers in a horizontal row, evenly spaced:
- Active contracts: 3
- This month's premiums: $720
- This month's payouts: $1,240
- Net: +$520 (in green)

Below, a clean table:

| Market                        | Strike      | Volume    | Premium  | Status                | Settlement |
|------------------------------|-------------|-----------|----------|-----------------------|------------|
| Atlanta Diesel — Mar 24      | Above $4.80 | 2,000 gal | $120     | TRIGGERED +$340       | Mar 25     |
| Atlanta Diesel — Mar 31      | Above $5.10 | 2,000 gal | $240     | ACTIVE                | Apr 1      |
| Atlanta Diesel — Apr Monthly | Above $5.00 | 3,000 gal | $360     | ACTIVE                | May 1      |

Status column: "TRIGGERED +$340" in green, "ACTIVE" in blue, "EXPIRED" in gray.

---

## Technical notes:
- Single index.html file with inline CSS and JS. No external dependencies except Google Fonts.
- Tab switching via JS — show/hide divs, no page reloads.
- The price chart can be a simple SVG with hardcoded path data. It doesn't need to be interactive — just visually represent a price trend.
- All data is hardcoded. This is a visual demo, not a working app.
- Make it responsive — should look decent on mobile with the two-column layout stacking vertically.
- Total code should be under 800 lines. If it's getting longer, you're overdesigning.
