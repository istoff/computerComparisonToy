# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Computer Evolution Comparison Tool** - an interactive web application that demonstrates the evolution of computing power from the 1940s to today through mathematically accurate comparisons and intelligent visualizations. The tool provides educational insights into 80+ years of computing history through precise calculations and contextual comparisons.

## Architecture

### Single-File Application
- **`compare.html`**: Complete self-contained application (HTML, CSS, JavaScript)
- **Pure web technologies**: No external dependencies or build process
- **Client-side only**: Runs entirely in the browser

### Core Data Structure
The application centers around a comprehensive `computers` object containing 60+ systems:
- **Historical Range**: ENIAC (1946) to Apple M4 (2024)
- **Categories**: Early computers, space computers, personal computers, mobile devices, gaming consoles, supercomputers, fictional computers
- **Specifications**: CPU specs (MHz, cores, IPC), memory, storage, power consumption, weight, cost
- **Calculated Metrics**: True computational power using `cores × MHz × IPC = MIPS`

### JavaScript Architecture

#### Core Functions
- **`populateDropdowns()`**: Builds categorized computer selection interface
- **`displayComparison()`**: Main orchestrator for comparison calculations and display
- **`createVisualization(ratio, name1, name2, category)`**: Adaptive visualization engine with scale metaphors
- **`formatNumber(num)`**: Number formatting with B/M/K suffixes
- **`formatMemoryStorage(kb)`**: Intelligent unit conversion (KB → TB)
- **`getComparisonLanguage(category, isComputer1Better)`**: Context-aware comparison descriptions

#### Reference System Functions
- **`loadReferenceData()`**: Asynchronously loads JSON reference files
- **`createReferencePanel(computerId, computerName)`**: Generates expandable historical information panels
- **`toggleReference(computerId)`**: Handles expand/collapse of reference panels
- **`createScaleMetaphor(ratio, name1, name2)`**: Generates real-world scale comparison visualizations

#### Timeline System Functions
- **`createTimeline(comp1Id, comp2Id)`**: Generates interactive computing history timeline
- **`timelineMilestones`**: Data structure containing key computing milestones from 1946-2024

#### Smart Visualization System
Different chart types based on magnitude:
- **Small differences (2-20×)**: Proportional bar charts
- **Medium differences (20-1000×)**: Circle size comparisons  
- **Huge differences (1000×+)**: Scale acknowledgment with real-world metaphors (tennis ball vs house, moon vs Jupiter)

#### Reference Data Architecture
- **Modular JSON files**: Separate data files for different computer categories
- **Rich historical context**: Overview, significance, technical details, development history
- **Interactive panels**: Expandable UI components for detailed information
- **Scalable system**: Easy to add new reference material for additional computers

## Key Technical Concepts

### Computational Accuracy
- **True Performance Metric**: Uses MIPS (Million Instructions Per Second) instead of raw MHz
- **Architecture Awareness**: Accounts for cores, instruction sets (8/16/32/64-bit), and IPC values
- **Multi-core Impact**: Demonstrates why modern dual-core processors outperform old single-core systems
- **Power Efficiency**: MIPS per Watt calculations for energy comparisons

### Educational Features
- **Mathematical Precision**: All ratios and comparisons are mathematically accurate
- **Contextual Language**: Uses appropriate descriptive terms ("lighter/heavier", "more/less efficient")
- **Historical Context**: Spans from room-sized computers to pocket devices
- **Interactive Timeline**: Visual computing history from 1946-2024 highlighting compared computers and key milestones
- **Fictional Integration**: Includes sci-fi computers (HAL 9000, Skynet, Enterprise) with plausible specifications

### Data Schema
Each computer entry contains:
```javascript
{
    name: "Computer Name (Year)",
    year: 1984,
    cpu: 25,        // MHz
    cores: 1,
    bits: 32,       // Architecture width
    ipc: 1.2,       // Instructions per cycle
    compute_power: 30,  // MIPS (calculated)
    memory: 1024,   // KB
    storage: 10240, // KB
    weight: 5.5,    // kg
    power: 85,      // Watts
    cost: 2500,     // USD
    category: "Personal Computer"
}
```

## Development Patterns

### Adding New Computers
1. Research accurate specifications for the system
2. Calculate true computational power using the MIPS formula
3. Add entry to appropriate category in the `computers` object
4. Ensure specifications follow the established schema
5. Test comparison functionality with edge cases

### Modifying Visualizations
- Visualization logic is in `createVisualization()` function
- Ratio thresholds determine which visualization type to use
- Each visualization type has specific DOM generation logic
- Consider accessibility and clarity when modifying visual elements

### Updating Comparison Logic
- Core comparison logic is in `displayComparison()` function
- Handles four main UI sections: summary, computation, visualization, specifications
- Ratio calculations must handle zero values and edge cases
- Language generation should be contextually appropriate

## File Structure
```
computerComparisonToy/
├── compare.html          # Main application with enhanced features
├── readme.md            # Project documentation
├── changelog.md         # Version history and features
├── CLAUDE.md           # This file
└── references/          # Reference material data files
    ├── early-computers.json    # Historical info for ENIAC, UNIVAC, IBM 704
    ├── space-computers.json    # Apollo, Voyager, Space Shuttle computers
    └── scale-comparisons.json  # Real-world objects for scale metaphors
```

## Running the Application

### Local Development
```bash
# Open in browser - no build process required
open compare.html
# or
python -m http.server 8000  # if serving locally needed
```

### Testing
- Test comparison accuracy with known systems
- Verify visualization scaling for different ratio ranges
- Check edge cases (zero values, extreme ratios)
- Validate historical accuracy of computer specifications

## Important Implementation Details

### Mathematical Precision
The application prioritizes accuracy over simplicity:
- Uses real-world specifications from historical sources
- Calculates true computational performance accounting for architecture differences
- Provides exact ratios rather than approximations
- Shows both human-readable and precise values

### Educational Design Philosophy
- **Accuracy First**: No misleading metaphors or "poetic" comparisons
- **Clarity Over Complexity**: Smart visualization selection based on data magnitude
- **Historical Context**: Demonstrates the true scale of technological progress
- **Tangible Understanding**: Makes abstract performance numbers comprehensible

### Browser Compatibility
- Uses modern JavaScript (ES6+) features
- CSS Grid and Flexbox for responsive layout
- No polyfills or compatibility layers
- Designed for modern browsers (Chrome, Firefox, Safari, Edge)

## Common Development Tasks

### Adding Computer Categories
1. Add new category to the computers database
2. Update `populateDropdowns()` if special grouping needed
3. Test dropdown organization and sorting
4. Verify comparison language works with new category

### Adding Reference Material
1. Create new JSON file in `references/` directory following the established schema
2. Add reference entries for computers using the standard format:
   - `overview`, `historical_significance`, `technical_details`, `development`, `interesting_facts`, `legacy`
3. Update `loadReferenceData()` function to include new reference file
4. Test expandable panels and ensure proper formatting

### Enhancing Scale Visualizations
1. Add new scale objects to `scale-comparisons.json` in appropriate size categories
2. Update emoji mappings in `createScaleMetaphor()` function
3. Adjust size calculation logic for new scale ranges
4. Test metaphor generation for different ratio ranges

### Modifying Performance Calculations
1. Update calculation logic in `displayComparison()`
2. Ensure formula display matches actual calculations
3. Test with edge cases and extreme values
4. Verify power efficiency calculations remain accurate

### Enhancing Visualizations
1. Modify `createVisualization()` function
2. Consider ratio thresholds for different visualization types
3. Update scale metaphor integration for large differences
4. Ensure accessibility and visual clarity
5. Test with various screen sizes and devices

### Working with Timeline
1. Add new milestones to `timelineMilestones` array with year, id, name, description, and type
2. Types available: 'milestone' (key breakthroughs), 'context' (supporting events), 'comparison' (auto-generated)
3. Timeline intelligently selects 8-10 items to avoid clutter
4. Compared computers are automatically highlighted in red
5. Key milestones pulse with orange highlighting