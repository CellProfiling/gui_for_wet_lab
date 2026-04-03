# gui_for_wet_lab

Simple GUI tools to simplify wet-lab experiment setup and sample preparation.

This repository collects small, lightweight GUI tools designed to help with common wet-lab workflows such as plate layout design and experiment metadata organization.

## Available Tools

### Plate Layout to Metadata
 
Design 384-well plate layouts and export structured per-well metadata. Built for single-cell proteomics LC-MS/MS workflows, but usable for any plate-based experiment.
 
See [tools/plate_layout_to_metadata/](tools/plate_layout_to_metadata/) for details and usage.
 
### Xcalibur Sequence Generator
 
Generate Xcalibur LC-MS sequence files from 384-well plate metadata. Takes the output of the Plate Layout to Metadata tool as input. Supports QC bracketing, seeded randomisation, and replicate balance checking.
 
See [tools/xcalibur_sequence_generator/](tools/xcalibur_sequence_generator/) for details and usage.

## Future Tools

Additional GUI utilities for wet-lab workflows will be added over time.
