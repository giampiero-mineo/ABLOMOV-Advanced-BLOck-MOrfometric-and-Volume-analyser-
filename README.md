# ABLOMOV-Advanced-BLOck-MOrfometric-and-Volume-analyser-
This Python project is a dedicated, modular solution for the quantitative 3D morphometric analysis of point cloud data, 
primarily designed for characterizing the size and shape distribution of rock blocks. It implements established geometric 
methods to derive Convex Hull properties and specific, widely-used morphometric indices

Project Architecture and Core Methodology
The code is structured into clear, logical modules to ensure high maintainability and testability: data_structures.py (types and constants), processing_core.py (pure calculation logic), 
and plot_output.py (visualization and I/O).The core analytical pipeline ensures robust parameter calculation:Convex Hull (CH) Derivation: The minimum convex envelope for each point cloud is computed using scipy.spatial.ConvexHull. 
The output is wrapped into a watertight trimesh.Trimesh object to reliably extract Volume and Surface Area through standard geometric measures. 
Dimensional Indices: The Flattening Coefficient (F) is derived from the ratio of the intermediate axis (W_ombb) to the shortest axis (T_ombb) of the Oriented Minimum Bounding Box (OMBB) which inscribes the object.
Chord Analysis and Morphometric Indices (alpha, beta): The critical shape indices are derived from the analysis of vectors (chords) connecting vertex pairs. The Alpha index is a ratio of surface area and volume, 
normalized by the mean chord length (Lavg). The Beta index quantifies the preferred particle orientation by analyzing the co-orientation of the longest chords (those above the median length) via their normalized dot products.
Efficiency Management: Chord analysis has an inherent (N^2) complexity. 
To manage performance for large datasets, the processing employs random vertex sampling, limiting the calculation to a maximum of 25,000 vertices (MAX_VERTICES_FOR_CHORD_CALC).

Data Presentation and Output
The output module focuses on accessible and informative data delivery:Triangular Diagram: The TriangularDiagramPlotter class maps beta (linearly, Y-axis) and the composite alpha \cdot F (logarithmically, X-axis) 
to Cartesian space, enabling visual classification within predefined shape regions (Cubic, Cubic-to-Elongated, Elongated, Elongated-to-Platy, Platy, Platy-to-Cubic).
Volume Classification: Data points are sized on the plot according to their Convex Hull volume. 
Volume classes are derived either from standard frequency percentiles or from custom user-defined cumulative volume thresholds, offering a third dimension of information. 
Export: All primary results, including Convex Hull properties and Morphometric Indices, are exported to detailed Excel (.xlsx) reports using the pandas library, facilitating external analysis and reporting.

Technical Requirements and Execution
The project requires Python 3.8+ and dependencies listed in requirements.txt (numpy, scipy, trimesh, laspy, pandas, matplotlib).
To run the analysis:Place input files (.las, .obj, .txt) in the designated input directory.Execute the main orchestration script: python main.py.The final processed data and visualizations are saved to the specified output directory.

Reference
Mineo G., Riquelme A., Rosone M., Cappadonia C. 
Integrating 3D Point Cloud analysis for unstable rock blocks characterization: a method for assessing size and shape distribution

Input Data Requirements
Point Clouds in .txt, .obj or .las format

Usage
See attached pdf file with "workflow_ABLOMOV"

License
This project is distributed under the GNU General Public License v3.0. See the full license: https://www.gnu.org/licenses/gpl-3.0.html

Disclaimer
Copyright (C) 2025 Giampiero Mineo
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <https://www.gnu.org/licenses/>.

Contact
Giampiero Mineo
Department of Earth and Marine Sciences,
University of Palermo,
Via Archirafi 22, Palermo 90123, Italy
Email: giampiero.mineo@unipa.it
mineogiampiero@gmail.com
