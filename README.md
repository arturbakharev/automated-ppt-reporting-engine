# Automated Data-to-PPTX Reporting Engine

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Status](https://img.shields.io/badge/Status-Production_Ready-success.svg)
![Proprietary](https://img.shields.io/badge/License-Proprietary-red.svg)

> **Note:** The core source code for this repository is kept private to protect proprietary data-parsing algorithms and custom workarounds developed for python-pptx library limitations. Below is a demonstration of the system's architecture, capabilities, and business impact.

## System Demonstration

**Click the image below to watch the video demonstration on YouTube:**

[![Automated Data-to-PPTX Demo](https://img.youtube.com/vi/wjLAdcW3o60/maxresdefault.jpg)](https://youtu.be/wjLAdcW3o60 "Click to Watch the Demo")

### The Transformation: Before vs. After
*How a blank template is programmatically populated with calculated metrics, dynamic boundaries, and perfectly aligned text fields.*

<table align="center">
  <tr>
    <th align="center">❌ Before (Static Template)</th>
    <th align="center">✅ After (Automated Output)</th>
  </tr>
  <tr>
    <td align="center"><img src="assets/before.jpg" alt="Before Program" width="450"/></td>
    <td align="center"><img src="assets/after.jpg" alt="After Program" width="450"/></td>
  </tr>
</table>


## Business Impact & Performance
This project was engineered to solve a complex, recurring business bottleneck: automating the generation of analytical reports based on large-scale sociological surveys containing **70,000+ respondents**. 
### The Challenge:
Reporting required data to be aggregated regionally, dictating a strict "one slide per region" format. Each slide needed to display identical variables but highly dynamic localized values (text blocks, region names, and charts). The primary architectural constraint was that survey questions and client data requirements changed monthly, rendering static PowerPoint templates entirely useless.
### The Solution:
I developed a full-stack desktop application featuring an interactive canvas where analysts can visually drag-and-drop text fields, charts, and variables. Once the layout is designed, the engine automatically iterates through the dataset and generates slides for all regions, perfectly replicating the user's custom layout pixel-by-pixel.

* **Massive Throughput:** Seamlessly ingests and processes **100MB+** of raw tabular data (SPSS `.sav` and Excel `.xlsx`).
* **Extreme Efficiency:** Generates comprehensive, dynamically styled **200+ slide** PowerPoint presentations in under **3 minutes**.
* **Labor Reduction:** Replaces approximately **2 weeks of manual labor** for two senior analysts, completely eliminating human error in complex data entry workflows.

## Engineered Features & Technical Highlights
1. **Interactive Canvas & Coordinate Projection:** Engineered a custom graphical scene (`QGraphicsScene`) for free-form UI element arrangement. Developed a highly precise mathematical projection algorithm that dynamically recalculates UI screen pixels into physical PowerPoint metrics (Inches/EMU). This ensures absolute layout fidelity between the frontend canvas and the final generated `.pptx` slides.
2. **Interactive Chart Pre-rendering:** Built a pre-render dialogue interface for complex visual data (e.g., Bubble and Line charts). Users can dynamically control text labels and visually filter out statistical outliers using an interactive slider prior to the final PPTX rendering phase.
3. **SPSS-Style Statistical Engine:** Integrated a custom formula syntax parser directly into the text fields. The system evaluates complex custom functions (e.g., categorical share distribution `share(var, [codes])` or weighted means `mean(var)`) and automatically computes accurate sociological metrics utilizing dynamic dataset weights.
4. **State Management & JSON Serialization:** The application state—including object coordinates, projection mappings, and layout configurations—is serialized into JSON. Implemented a robust background autosave routine (every 30 seconds) and a crash-recovery mechanism to prevent data loss.

## Tech Stack Overview
* **Backend Engine:** Python (Pandas for heavy data manipulation, `pyreadstat` for SPSS parsing, `BeautifulSoup4` for HTML style extraction, custom Regex engines for formula validation, and `python-pptx` for low-level Office Open XML generation).
* **Frontend Architecture:** PyQt6 (leveraging `QGraphicsScene` and `QGraphicsView` for the interactive canvas, alongside custom-built widgets for color palettes, formula constructors, and dynamic chart previews).
* **Performance Optimization:** Asynchronous UI event handlers and strict memory management protocols, including forced Garbage Collection (GC) sweeps every 10 slide iterations, ensuring absolute stability when parsing large-scale datasets.
