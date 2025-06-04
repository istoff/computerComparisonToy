# Changelog

All notable changes to the Computer Evolution Comparison Tool will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.1] - 2024-06-04

### 🐛 Critical Bug Fixes - Performance Summary Accuracy

#### Fixed
- **Performance Summary Logic**: Fixed widespread bug where comparison results were inverted
  - Previously: "Snapdragon 8 Gen 2 Phone is less powerful" (when it was actually more powerful)
  - Now: "Snapdragon 855 Phone is less powerful" (correctly describing computer1 vs computer2)
- **Grammar Issues**: Fixed "is has" construction in comparison descriptions
  - Before: "Computer is has more storage"
  - After: "Computer has more storage"
- **Consistent Evaluation Logic**: Now properly evaluates "Is computer1 better than computer2?" 
  - Always describes computer1's relationship to computer2
  - Handles both higher-is-better (compute, memory, storage) and lower-is-better (power, weight) metrics correctly
- **Power/Weight Comparisons**: Removed double-negation logic that caused efficiency and weight comparisons to be backwards

#### Technical Details
- Simplified comparison logic to consistently evaluate computer1 vs computer2
- Removed confusing "better computer" selection that mixed up which system was being described
- Fixed unit consistency in all comparison evaluations

## [2.0.0] - 2024-06-04

### 🎉 Major Redesign - Clean, Smart Visualizations

#### Added
- **Smart Visualization System**: Different chart types based on difference magnitude
  - Small differences (2-20×): Simple side-by-side bars
  - Medium differences (20-1000×): Proportional circle comparisons  
  - Huge differences (1000×+): Scale acknowledgment with clear messaging
- **Comprehensive Computer Database**: 60+ computers from 1946-2024
  - Early computers (ENIAC, UNIVAC)
  - Complete Intel evolution (8086 → Core i9)
  - AMD processors (Athlon → Ryzen 9)
  - Apple Silicon (M1 → M4)
  - ARM/Mobile (Snapdragon series)
  - Space computers (Apollo, Voyager, Shuttle)
  - Gaming consoles (NES → PlayStation 5)
  - Supercomputers (Cray-1 → Frontier)
  - **Fictional computers**: HAL 9000, Skynet, Enterprise, Jurassic Park SGI, WOPR, Mother
- **Intelligent Unit Conversion**: 
  - Memory/Storage: KB → MB → GB → TB with original values in brackets
  - Automatic unit selection based on magnitude
- **Contextual Language**: Proper comparative descriptions
  - "Lighter/heavier" for weight
  - "More/less power efficient" for power consumption
  - "More powerful/less powerful" for computation
- **Compact Information Layout**:
  - Summary grid showing key ratios upfront
  - Computational breakdown with clear formulas
  - Clean spec cards with organized information

#### Changed
- **Complete Interface Redesign**: Cleaner, more readable layout
- **Visualization Logic**: Charts now scale appropriately to difference magnitude
- **Performance Summary**: Uses appropriate comparative language instead of generic "faster"
- **Spec Display**: Better organized with proper unit formatting

### Removed
- Cluttered multi-visual displays that were hard to interpret
- Confusing pixel visualizations for small differences
- Generic "faster" language for all comparisons

## [1.5.0] - 2024-06-03

### 🧠 Accurate Computational Metrics

#### Added
- **True Computational Power Calculation**: Cores × MHz × IPC = MIPS
- **Architecture Details**: Core count, bit width (8/16/32/64-bit), IPC values
- **Power Efficiency Metrics**: MIPS per Watt calculations
- **Multi-core Impact Visualization**: Shows why modern dual-core beats old single-core
- **Detailed Computation Breakdown**: Formula display showing exact calculations

#### Changed
- **Replaced Raw MHz with MIPS**: More accurate performance representation
- **Enhanced Computer Specifications**: Added cores, IPC, and bit width for all systems
- **Improved Comparisons**: Now account for architectural differences beyond clock speed

#### Fixed
- **Misleading Performance Metrics**: Raw MHz comparisons that ignored multi-core and IPC
- **Historical Accuracy**: Better representation of actual computational capabilities

## [1.0.0] - 2024-06-02

### 🎯 Mathematically Accurate Metaphors

#### Added
- **Precise Scale References**: Real-world objects with accurate measurements
- **Multiple Visualization Types**: Bar charts, square comparisons, pixel representations
- **Comprehensive Metaphor System**: Physics-based analogies with correct ratios
- **Visual Scale Representations**: Different methods for different magnitude ranges
- **Real Computer Database**: Initial set of historically significant computers

#### Changed
- **Metaphor Accuracy**: Replaced poetic comparisons with mathematically precise ones
- **Scale Representation**: Ensured all visual elements reflect true proportions

#### Fixed
- **Inaccurate Analogies**: Removed metaphors that didn't match actual ratios (e.g., "candle to hair dryer" for 5× difference)

## [0.5.0] - 2024-06-01

### 🚀 Initial Concept

#### Added
- **Basic Computer Comparison**: Simple side-by-side specifications
- **Initial Database**: Small set of iconic computers
- **Raw Specifications Display**: CPU speed, memory, storage comparisons
- **Simple Metaphor System**: Basic analogies for scale differences

#### Features
- Interactive computer selection
- Basic specification comparison
- Simple ratio calculations
- Rudimentary visualizations

---

## Future Roadmap

### [3.0.0] - Planned
- **Quantum Computer Integration**: IBM Q, Google Sycamore comparisons
- **GPU Comparison Module**: Graphics processing evolution
- **Timeline Visualization**: Historical progression view
- **Performance Benchmarks**: Real-world performance data integration
- **Mobile App**: Native mobile application

### [2.5.0] - Planned  
- **Enhanced Fictional Computers**: More sci-fi systems with detailed specs
- **Cost Analysis**: Inflation-adjusted price comparisons over time
- **Energy Deep-dive**: Environmental impact calculations
- **Export Features**: Share comparisons, generate reports

### [2.1.0] - Planned
- **Search Functionality**: Find computers by name, year, or specs
- **Favorites System**: Save interesting comparisons
- **Comparison History**: Track previous comparisons
- **Improved Mobile Experience**: Touch-optimized interface

### 🎉 Major Redesign - Clean, Smart Visualizations

#### Added
- **Smart Visualization System**: Different chart types based on difference magnitude
  - Small differences (2-20×): Simple side-by-side bars
  - Medium differences (20-1000×): Proportional circle comparisons  
  - Huge differences (1000×+): Scale acknowledgment with clear messaging
- **Comprehensive Computer Database**: 60+ computers from 1946-2024
  - Early computers (ENIAC, UNIVAC)
  - Complete Intel evolution (8086 → Core i9)
  - AMD processors (Athlon → Ryzen 9)
  - Apple Silicon (M1 → M4)
  - ARM/Mobile (Snapdragon series)
  - Space computers (Apollo, Voyager, Shuttle)
  - Gaming consoles (NES → PlayStation 5)
  - Supercomputers (Cray-1 → Frontier)
  - **Fictional computers**: HAL 9000, Skynet, Enterprise, Jurassic Park SGI, WOPR, Mother
- **Intelligent Unit Conversion**: 
  - Memory/Storage: KB → MB → GB → TB with original values in brackets
  - Automatic unit selection based on magnitude
- **Contextual Language**: Proper comparative descriptions
  - "Lighter/heavier" for weight
  - "More/less power efficient" for power consumption
  - "More powerful/less powerful" for computation
- **Compact Information Layout**:
  - Summary grid showing key ratios upfront
  - Computational breakdown with clear formulas
  - Clean spec cards with organized information

#### Changed
- **Complete Interface Redesign**: Cleaner, more readable layout
- **Visualization Logic**: Charts now scale appropriately to difference magnitude
- **Performance Summary**: Uses appropriate comparative language instead of generic "faster"
- **Spec Display**: Better organized with proper unit formatting

### Removed
- Cluttered multi-visual displays that were hard to interpret
- Confusing pixel visualizations for small differences
- Generic "faster" language for all comparisons

## [1.5.0] - 2024-06-03

### 🧠 Accurate Computational Metrics

#### Added
- **True Computational Power Calculation**: Cores × MHz × IPC = MIPS
- **Architecture Details**: Core count, bit width (8/16/32/64-bit), IPC values
- **Power Efficiency Metrics**: MIPS per Watt calculations
- **Multi-core Impact Visualization**: Shows why modern dual-core beats old single-core
- **Detailed Computation Breakdown**: Formula display showing exact calculations

#### Changed
- **Replaced Raw MHz with MIPS**: More accurate performance representation
- **Enhanced Computer Specifications**: Added cores, IPC, and bit width for all systems
- **Improved Comparisons**: Now account for architectural differences beyond clock speed

#### Fixed
- **Misleading Performance Metrics**: Raw MHz comparisons that ignored multi-core and IPC
- **Historical Accuracy**: Better representation of actual computational capabilities

## [1.0.0] - 2024-06-02

### 🎯 Mathematically Accurate Metaphors

#### Added
- **Precise Scale References**: Real-world objects with accurate measurements
- **Multiple Visualization Types**: Bar charts, square comparisons, pixel representations
- **Comprehensive Metaphor System**: Physics-based analogies with correct ratios
- **Visual Scale Representations**: Different methods for different magnitude ranges
- **Real Computer Database**: Initial set of historically significant computers

#### Changed
- **Metaphor Accuracy**: Replaced poetic comparisons with mathematically precise ones
- **Scale Representation**: Ensured all visual elements reflect true proportions

#### Fixed
- **Inaccurate Analogies**: Removed metaphors that didn't match actual ratios (e.g., "candle to hair dryer" for 5× difference)

## [0.5.0] - 2024-06-01

### 🚀 Initial Concept

#### Added
- **Basic Computer Comparison**: Simple side-by-side specifications
- **Initial Database**: Small set of iconic computers
- **Raw Specifications Display**: CPU speed, memory, storage comparisons
- **Simple Metaphor System**: Basic analogies for scale differences

#### Features
- Interactive computer selection
- Basic specification comparison
- Simple ratio calculations
- Rudimentary visualizations

---

## Future Roadmap

### [3.0.0] - Planned
- **Quantum Computer Integration**: IBM Q, Google Sycamore comparisons
- **GPU Comparison Module**: Graphics processing evolution
- **Timeline Visualization**: Historical progression view
- **Performance Benchmarks**: Real-world performance data integration
- **Mobile App**: Native mobile application

### [2.5.0] - Planned  
- **Enhanced Fictional Computers**: More sci-fi systems with detailed specs
- **Cost Analysis**: Inflation-adjusted price comparisons over time
- **Energy Deep-dive**: Environmental impact calculations
- **Export Features**: Share comparisons, generate reports

### [2.1.0] - Planned
- **Search Functionality**: Find computers by name, year, or specs
- **Favorites System**: Save interesting comparisons
- **Comparison History**: Track previous comparisons
- **Improved Mobile Experience**: Touch-optimized interface