# FastForward Ops Dashboard — Project Brief

An internal executive dashboard for FastForward Logistics, a mid-size freight and supply chain company. Built for the VP of Operations to review business performance in leadership meetings: shipment volume, on-time delivery rates, regional performance, and open exceptions, all on one screen.

## Tech
- Vue 3 via Vite, with TypeScript and Vue Router
- No Pinia, no testing setup, no JSX, no ESLint/Prettier for now
- Vuetify 3 as the component library (app bar, cards, grid)
- Deploys to Vercel as a static/SPA build

## Design
- Dark mode by default, consistent with a glassmorphism aesthetic: semi-transparent cards, subtle blur, softly rounded corners
- Background with a slow-moving gradient and bokeh-style shapes, understated so it doesn't compete with the data
- Typography: Montserrat, mixing Bold for headings/key numbers and Ultra Light for labels and secondary text
- Grid layout: header/app bar, then a responsive grid of metric cards, with room for a chart section below
- Should feel calm and executive-ready, not flashy — data-first, not decorative-first

## Data (to be finalized in Step 2.4)
- Mock dataset in src/data/metrics.json: shipment volume, on-time delivery %, regional performance breakdown, count of open exceptions
- At least one interactive filter (date range or region selector) that updates the visible data

## Nice to have
- Reusable MetricCard component with props for label, value, and trend direction (up/down indicator)
- Icons on metric cards (simple SVG or icon set from Vuetify)
- Footer with build/version note