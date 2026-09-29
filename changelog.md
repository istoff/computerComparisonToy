# Changelog

All notable changes to the Computer Evolution Comparison Tool will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.3.0] - 2026-09-29

### 📱 Modern Phones, Memory Sliders, Searchable Picker

#### Added — 7 current phones
- iPhone 17 Pro and iPhone Air (A19 Pro, 2025), iPhone 18 Pro (A20 Pro, 2 nm, 2026)
- Samsung Galaxy S25 Ultra (2025) and S26 Ultra (Snapdragon 8 Elite Gen 5, 2026)
- Google Pixel 10 Pro (Tensor G5, 2025) and Pixel 11 Pro (Tensor G6, 2026)

Each carries bandwidth, memory architecture and hardware decoder counts, so they get the same workload estimates as everything else.

#### Added — memory sliders in "What each one could run"
Each machine gets a slider stepping through the memory configurations it actually shipped in — 96 / 256 / 512 GB for a Mac Studio M3 Ultra, 24 / 48 / 64 GB for a Mac mini M4 Pro, 32 / 64 / 128 GB for a Ryzen AI Max+ 395. Moving it recomputes the largest model that fits, the token rate and the datasheet memory row live. Machines with one soldered size say so instead of showing a dead control. 48 machines have options; `memory_options` is the new field.

#### Changed — 9 duplicate entries collapsed
The separate base and maxed-out entries added in 2.2.0 (Mac mini M4 16GB *and* 32GB, Mac Studio M3 Ultra 96GB *and* 512GB, and so on) are now one entry each with a slider covering the range. The list is shorter and the search is cleaner; nothing is lost, since every configuration is still reachable. 139 entries down to 130.

#### Added — searchable machine picker
The two dropdowns are now comboboxes. Type to filter across name, maker, category and year — "ultra", "1977" and "phone" all work, with matches underlined. Results are grouped into five families rather than fifteen flat categories, newest first, with each row showing category and memory:

- Phones and tablets · Desktops and laptops · AI machines and big iron · Historic · Small and imagined

Filter chips narrow to one family; "Build your own" opens the custom-build panel. Full keyboard support (arrows, Enter, Escape) with `aria-activedescendant`, and the original `<select>` elements stay in the DOM as the source of truth so nothing downstream changed.

#### Fixed
- Selecting a saved custom build reopened the custom-build panel instead of comparing it, because two options shared the `custom_build_N` value. The picker now calls the panel directly and the value is only ever a real machine.
- The datasheet price row now names the memory configuration it refers to when a machine has several.

## [2.2.0] - 2026-09-29

### ⚙️ Workload Estimates, Whole-Machine Power, New Interface

#### Added — "What each one could run"
Three estimates derived from the specs, each shown only when it has something to say:
- **Largest language model that fits** — usable memory at 75% of total, 4-bit weights at 0.55 bytes/parameter, matched against a ladder of real models from Qwen2.5 0.5B to DeepSeek-R1 671B
- **Token generation** — bandwidth ÷ model size, at 72% efficiency on unified memory and 45% on system RAM, with the slower machine indexed at 100%. Appears only when both machines have a bandwidth figure and a model that fits in both
- **1080p30 H.264 decode** — software streams scaled from instruction throughput at 2,500 MIPS per stream, plus the fixed-function decoder count

#### Added — two new spec fields
- `bandwidth` (GB/s) and `mem_arch` (`unified` / `ddr`) on 81 entries
- `gpu_decode` (simultaneous 1080p30 H.264 streams) on 76 entries — including the Raspberry Pi 5, which dropped H.264 hardware decode

#### Added — memory configurations
Machines with wide memory ranges now appear as the configuration people actually buy and the configuration that matters for AI work: Mac mini M4 / M4 Pro / M6 / M5 Pro, Mac Studio M4 Max / M3 Ultra / M5 Max / M5 Ultra, Ryzen AI Max+ 395. Names and prices reflect the configuration.

#### Merged with the phone and tablet work
This release merges the branch that added 18 phones and tablets (iPhone 15 Pro, Galaxy S3 through S24 Ultra, the Pixel line, iPads, Surface Pro, Kindle Fire), embedded the reference JSON inline so the page works over `file://`, and renamed `compare.html` to `index.html`. Those machines now carry `bandwidth`, `mem_arch` and `gpu_decode` too, so they get the same workload estimates. The database is **132 systems**, and the `computers` object is now emitted grouped by category with a comment per group.

The Apollo and Voyager corrections were applied to the embedded copy of the reference data as well as to `references/space-computers.json` — the inline copy still carried the old "4KB ROM + 2KB RAM" figure.

#### Changed — power is now whole-machine
Every `power` value is the draw of the complete machine under load, not CPU package TDP. Affects 26 entries: a 14900K PC went from 253 W to 620 W, an EPYC 9754 node from 360 W to 700 W, a MacBook Pro M4 Max from 48 W to 140 W. MIPS-per-watt is now comparable across eras.

#### Changed — interface rebuilt
- **Decade ruler as the lead** — both machines plotted on a base-10 axis of instructions per second. The axis spans the whole database by default and zooms in when the two machines sit within four decades of each other
- Teal for Machine A, amber for Machine B, carried through every section including the timeline
- Space Grotesk for display, IBM Plex Sans for data, IBM Plex Mono for the formula; tabular figures throughout
- Light and dark themes, responsive to mobile, keyboard focus visible, reduced motion respected
- Emoji headings, gradient background and card shadows removed

#### Changed — timeline
- Extended to 2026 and rewritten: 28 milestones including the transformer paper, exascale, and 2 nm silicon
- Defaults to the window around the two compared machines and scrolls to them; "Show all years" opens the full span
- Removed the `Math.random()` milestone selection that reshuffled the timeline on every redraw
- Compared machines are marked in their own colour rather than a generic red

#### Changed — custom builds
Memory bandwidth, memory architecture and hardware decoder count are now editable, so a custom build gets the same workload estimates as a stock machine. Loading a preset fills them in.

#### Fixed
- Scale metaphors were re-randomised on every redraw; they are now deterministic for a given ratio
- Memory and storage no longer print a redundant KB figure next to TB and PB values; sub-kilobyte memory now reads in bytes rather than rounding to zero
- Price is shown in the datasheet, which previously omitted it

## [2.1.0] - 2026-09-29

### 🔍 Spec Accuracy Audit + AI-Era Hardware

#### Fixed — unit and magnitude errors in the `computers` database
- **ENIAC**: `cpu` was 0.0001 MHz (100 Hz); ENIAC's clock was 100 kHz → `cpu: 0.1`. `cores × MHz × IPC` now actually equals the stated 0.005 MIPS (it was off by 1000×, the only formula mismatch in the database)
- **UNIVAC I**: memory 1 KB → 12 KB (1,000 words × 12 characters); throughput corrected to ~0.0019 MIPS (~1,905 instr/sec) at its real 2.25 MHz clock
- **Apollo Guidance Computer**: 1.024 MIPS → 0.086 MIPS (AGC ran ~43k–85k instructions/sec); ROM 36 KB → 72 KB (36,864 × 16-bit words)
- **Voyager**: 4 MHz → 0.25 MHz (real CCS clock), 2.4 MIPS → 0.008 MIPS; weight 4.2 kg → 30 kg (CCS + FDS + AACS)
- **Space Shuttle GPC**: 0.98 MIPS → 0.42 MIPS (AP-101B was ~480 KIPS)
- **Cray-1**: memory 8,388,608 KB (8 GB) → 8,192 KB (8 MB — 1M × 64-bit words)
- **Cray-2**: memory 256 GB → 2 GB (256M × 64-bit words)
- **Deep Blue**: memory 1 TB → ~30 GB (no 1997 machine had 1 TB of RAM)
- **Frontier**: storage 700 EB → 700 PB (three extra zeros; El Capitan's entry already had it right)
- **El Capitan / Aurora**: power 21 MW / 20 MW → 29.6 MW / 38.7 MW (measured Top500/Green500 draw)
- **PlayStation 5**: 3800 MHz → 3500 MHz (Zen 2 @ 3.5 GHz variable)
- **Snapdragon 8 Gen 3**: 3400 MHz → 3300 MHz
- **NVIDIA Grace Hopper**: 3500 MHz → 3100 MHz (Grace Neoverse V2 max clock)
- **M4 Pro**: memory 48 GB → 64 GB (actual maximum configuration)

#### Added — AI Workstation category
New `AI Workstation` category for large-unified-memory machines bought to run models locally:
- Mac Studio M4 Max (2025) — 128 GB unified
- Mac Studio M3 Ultra (2025) — 512 GB unified, the largest unified memory on any personal computer at launch
- Mac Studio M5 Max (2026) — 128 GB unified, 614 GB/s
- Mac Studio M5 Ultra (2026) — 512 GB unified, 1.2 TB/s
- NVIDIA DGX Spark GB10 (2025) — 128 GB unified, 1 PFLOP FP4
- AMD Ryzen AI Max+ 395 "Strix Halo" mini PC (2025) — 128 GB unified, up to 96 GB addressable as VRAM

#### Added — Mac mini line
- Mac mini M4 (2024), Mac mini M4 Pro (2024)
- Mac mini M6 (2026), Mac mini M5 Pro (2026)

#### Added — Intel / AMD updates
- Ryzen 9 9950X3D PC (2025) — 16 cores, 5.7 GHz, 144 MB 3D V-Cache
- AMD EPYC 9965 Server (2024) — 192 Zen 5c cores, 500 W
- Intel Xeon 6980P Server (2024) — 128 P-cores, 500 W

#### Changed
- Custom Build category dropdown now offers every category in the database (Apple Silicon, ARM/Mobile, AI Workstation, Data Center Server were missing)
- Database grew from 92 to 105 systems

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