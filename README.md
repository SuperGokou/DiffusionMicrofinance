# The Diffusion of Microfinance

An interactive data visualization dashboard exploring household-level survey data on microfinance adoption patterns. Built with D3.js for CS171 - Data Visualization.

**[Live Demo](https://supergokou.github.io/THE-DIFFUSION-OF-MICROFINANCE/)**

![Dashboard Screenshot](screenshot.png)

---

## Overview

This dashboard visualizes survey data collected from households to understand the diffusion and adoption patterns of microfinance services. The visualization allows users to explore how different demographic and socioeconomic factors correlate with microfinance adoption over time.

### Key Features

- **Interactive Time Series**: Area chart displaying survey responses over time with brushing capability
- **Demographic Breakdowns**: Four bar charts showing distribution across key household characteristics
- **Linked Views**: Brush selection on the timeline automatically filters all bar charts
- **Smooth Transitions**: Animated updates when filtering data

---

## Visualizations

### Survey Timeline (Area Chart)
Shows the number of survey responses collected each day. Users can brush (click and drag) to select a date range, which filters the data displayed in all bar charts.

### Household Characteristics (Bar Charts)

| Chart | Description |
|-------|-------------|
| **Own or Rent** | Housing tenure status - whether households own, rent, or lease their homes |
| **Electricity** | Access to electricity - private connection, government supply, or none |
| **Latrine** | Sanitation facilities - owned, common/shared, or none |
| **Religion** | Religious affiliation of the household head |

---

## Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| D3.js | v6 | Data visualization, bindng, scales, axes, and brushing |
| Bootstrap | 4.5 | Responsive grid layout and base styling |
| jQuery | 3.5.1 | Bootstrap JavaScript dependency |
| Popper.js | 1.16.1 | Bootstrap tooltip/popover positioning |

---

## Project Structure

```
THE-DIFFUSION-OF-MICROFINANCE/
├── index.html                          # Main HTML entry point
├── css/
│   └── style.css                       # Custom dashboard styles
├── js/
│   ├── main.js                         # Data loading, chart initialization, brush handling
│   ├── areachart.js                    # Reusable AreaChart class with brushing
│   └── barchart.js                     # Reusable BarChart class with filtering
├── data/
│   └── household_characteristics.csv   # Survey dataset (3,400+ records)
├── fonts/
│   └── glyphicons-halflings-regular.*  # Bootstrap icon fonts
├── screenshot.png                      # Dashboard preview image
└── README.md                           # This file
```

---

## Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Edge, Safari)
- A local web server (required due to CORS restrictions when loading CSV data)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/supergokou/THE-DIFFUSION-OF-MICROFINANCE.git
   cd THE-DIFFUSION-OF-MICROFINANCE
   ```

2. **Start a local server**

   Using Python 3:
   ```bash
   python -m http.server 8000
   ```

   Using Node.js:
   ```bash
   npx serve
   ```

   Using VS Code:
   - Install the "Live Server" extension
   - Right-click `index.html` and select "Open with Live Server"

3. **Open in browser**

   Navigate to `http://localhost:8000` (or the port shown by your server)

---

## How to Use

1. **View Overall Distribution**: When the page loads, all charts display the complete dataset

2. **Filter by Time Period**:
   - Click and drag on the area chart to select a date range
   - All bar charts update to show only data from the selected period
   - Release the brush to maintain the selection

3. **Reset Filter**:
   - Click outside the brushed area on the area chart to clear the selection
   - All charts return to showing the full dataset

---

## Data Source

The dataset contains household-level survey responses with the following characteristics:
- **Survey Period**: July 2007
- **Total Records**: 3,432 households
- **Geographic Scope**: Rural communities in developing regions
- **Variables**: Survey date, housing tenure, electricity access, sanitation facilities, religious affiliation

---

## Architecture

### Design Pattern
The codebase follows a class-based MVC-like pattern:

- **Model**: CSV data loaded and transformed within each chart class
- **View**: D3.js SVG rendering in `updateVis()` methods
- **Controller**: Event handling through D3 brush interactions

### Chart Classes

Both `AreaChart` and `BarChart` follow a consistent structure:

```javascript
class Chart {
    constructor()   // Initialize with parent element and data
    initVis()       // Set up SVG, scales, axes (static structure)
    wrangleData()   // Transform/aggregate data for display
    updateVis()     // Binddata and render with transitions
}
```

### Interaction Flow

```
User brushes area chart
        ↓
brushed() callback in main.js
        ↓
Extracts date range from brush selection
        ↓
Calls selectionChanged() on each bar chart
        ↓
Bar charts filter data and re-render
```

---

## Browser Compatibility

Tested and working on:
- Google Chrome 90+
- Mozilla Firefox 88+
- Microsoft Edge 90+
- Safari 14+

---

## License

MIT License for code. Survey data is used for educational purposes only.

---

## Acknowledgments

- CS171 - Data Visualization course at Harvard University
- D3.js community for excellent documentation and examples
- Original survey data researchers
