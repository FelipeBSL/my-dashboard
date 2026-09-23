# FastForward Ops Dashboard — Project Brief

An internal executive dashboard for FastForward Logistics, a mid-size freight and supply chain company. Built for the VP of Operations to review business performance in leadership meetings: shipment volume, on-time delivery rates, regional performance, and open exceptions, all on one screen.

## Tech
- Vue 3 via Vite, with TypeScript and Vue Router
- No Pinia, no testing setup, no JSX, no ESLint/Prettier for now
- Vuetify 3 as the component library (app bar, cards, grid)
- Deploys to Vercel as a static/SPA build

## Layout
- A Vuetify app bar identifies FastForward Logistics and the dashboard context.
- The key metrics area uses reusable metric cards for shipment volume, on-time delivery, and open exceptions.
- Regional performance uses a specialized card with horizontal comparison bars.
- A monthly shipment-volume chart sits below the key metrics for leadership trend review.

## Design
- Dark mode by default, consistent with a glassmorphism aesthetic: semi-transparent cards, subtle blur, softly rounded corners
- Background with a slow-moving gradient and bokeh-style shapes, understated so it doesn't compete with the data
- Typography: Montserrat, mixing Bold for headings/key numbers and Ultra Light for labels and secondary text
- Grid layout: header/app bar, then a responsive grid of metric cards, with room for a chart section below
- Should feel calm and executive-ready, not flashy — data-first, not decorative-first

## Data
- Mock data lives in `src/data/metrics.json` and includes an overall summary, region-level metrics, trends, and a last-updated date.
- Regional values are intentionally varied to create a realistic leadership-review scenario: the South has the lowest on-time rate, while the West has the strongest performance.

## Interactions
- A region selector supports `All Regions`, Northeast, Midwest, South, and West.
- Changing the selector updates the metric cards, regional performance view, and monthly shipment trend.

## Style
- Dark, calm, executive-ready visual system with glassmorphism surfaces, Montserrat typography, restrained motion, and indigo/cyan data accents.
- Data remains the primary focus; background bokeh and gradients stay subtle behind the dashboard.

## Nice to have
- Reusable MetricCard component with props for label, value, and trend direction (up/down indicator)
- Icons on metric cards (simple SVG or icon set from Vuetify)
- Footer with build/version note