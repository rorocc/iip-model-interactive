# IIP Model Simulation

Interactive Simulation of the Integrated Information Processing Model by Schrills (2024) built with Vue 3 in Vite.

## Pipelines Status
[![Deploy static content to Pages](https://github.com/rorocc/iip-model-interactive/actions/workflows/deploy.yml/badge.svg)](https://rorocc.github.io/iip-model-interactive/)

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

## Project Structure

    .
    ├── ...
    ├── src
    │   ├── assets              # CSS, JSON data files for tooltip and scenario generation, and SVG files (not used in code, but as a fallback for future changes)
    │   ├── components          # Main components used throughout the project
    │   └── …
    └── ...

## Tooltips and Scenarios
### Modifying tooltips
To add interactive tooltips to the model, use the `src/assets/tooltips.json` file and adjust accordingly.
You need to provide the following fields:
- `tooltipId`: Identifier of the tooltip. Can be any name.
- `targetId`: The ID of the HTML element that triggers the tooltip on hover.
- `headline` (optional): Headline of the Tooltip.
- `text`: Descriptional text
The tooltips are then automatically generated in `src/components/iip-simulator.vue`.

### Modifiying scenarios
To add or adjust scenarios, use the `src/assets/scenarios.json` file and adjust accordingly.
You need to provide the following fields:
- `name`: Name of the scenario. Will be shown in the Select-element.
- `properties`:
  - `inputAdequacy` (Boolean)
  - `referenceConsonance` (Boolean)
  - `outputDiagnosticity` (Boolean)
- `tooltips`(optional):
  - For each tooltip, add the same fields as stated in the section about modifying tooltips.  
