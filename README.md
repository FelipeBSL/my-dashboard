# FastForward Ops Dashboard

An internal executive dashboard prototype for FastForward Logistics. It gives operations leadership one view of shipment volume, on-time delivery, regional performance, open exceptions, and monthly shipment trends.
# vue-scaffold-tmp

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VS Code](https://code.visualstudio.com/) + [Vue (Official)](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Recommended Browser Setup

- Chromium-based browsers (Chrome, Edge, Brave, etc.):
  - [Vue.js devtools](https://chromewebstore.google.com/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)
  - [Turn on Custom Object Formatter in Chrome DevTools](http://bit.ly/object-formatters)
- Firefox:
  - [Vue.js devtools](https://addons.mozilla.org/en-US/firefox/addon/vue-js-devtools/)
  - [Turn on Custom Object Formatter in Firefox DevTools](https://fxdx.dev/firefox-devtools-custom-object-formatters/)

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

## Stack

- Vue 3, TypeScript, Vite, and Vue Router
- Vuetify with Material Design Icons
- JSON mock data in `src/data/metrics.json`
- Static SPA build suitable for educational deployment on Vercel

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

### Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

### Validation and Production Build

```sh
npm run build
```

The build runs the Vue type-check and the Vite production build together.
## Dashboard Interaction

Use the region selector to switch between the overall view and Northeast, Midwest, South, or West. The selected region updates the metric cards, regional performance view, and monthly shipment trend.
## Structure

- `src/views/DashboardView.vue`: dashboard layout, filter state, and derived view data.
- `src/components/MetricCard.vue`: reusable card for standard KPI metrics.
- `src/data/metrics.json`: mock operational dataset and trend series.
- `src/assets/base.css`: global design tokens and base styles.

## Capstone Note

This project was created for the Protogen 200s Capstone. Vercel is used for educational deployment only and must not be used to release client or Slalom products.
