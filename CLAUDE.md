# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

jsMind is a pure JavaScript library for displaying and editing mind maps, built on HTML5 canvas and SVG. It's distributed under BSD-3-Clause license.

## Key Commands

### Development
- `npm run server` - Start local HTTP server for development
- `npm run build` - Build the library using Rollup (outputs to `es6/` directory)
- `npm run build-types` - Generate TypeScript declaration files

### Testing
- `npm run test` or `npm run test-es6` - Run ES6 module tests (unit tests)
- `npm run test-types` - Run TypeScript type tests
- `npm run build-test-types` - Build types and run type tests
- `npm run test-legacy` - Run legacy format tests

### Code Quality
- `npm run format` - Format code using Prettier
- `npm run format-check` - Check code formatting without modifying files

### Running a Single Test
To run a specific test file:
```bash
NODE_OPTIONS=--experimental-vm-modules jest tests/unit/specific-test-file.test.js
```

## Architecture Overview

The jsMind library follows a modular architecture with clear separation of concerns:

### Core Components
- **jsmind.js** - Main entry point and orchestrator that coordinates all other components
- **jsmind.mind.js** - Mind map data model (stores nodes, relationships)
- **jsmind.node.js** - Individual node implementation
- **jsmind.data_provider.js** - Handles data import/export in multiple formats
- **jsmind.layout_provider.js** - Calculates node positions and layout algorithms
- **jsmind.view_provider.js** - Renders the mind map using canvas/SVG
- **jsmind.shortcut_provider.js** - Keyboard shortcut handling

### Plugin System
- **jsmind.plugin.js** - Plugin infrastructure
- Plugins in `src/plugins/`:
  - `jsmind.draggable-node.js` - Drag and drop functionality
  - `jsmind.screenshot.js` - Screenshot export functionality

### Build Output
- Source files in `src/` are built to minified UMD modules in `es6/`
- TypeScript definitions are generated in `types/generated/`
- Three separate builds: main library, draggable-node plugin, screenshot plugin

### Data Formats
The library supports multiple mind map data formats for import/export, handled by the data provider and format modules.

## Important Notes

- The library uses Rollup for bundling with terser for minification
- All tests require `NODE_OPTIONS=--experimental-vm-modules` for ES6 module support
- The project maintains both ES6 modules and legacy support
- External dependencies for plugins: `dom-to-image` for screenshot functionality