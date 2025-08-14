# Binary TIFF Stack Interpolator

**Author:** Evan Troendle  
**Purpose:** Interpolate between consecutive binary image slices in a multi-page TIFF stack using perimeter- or area-based signed distance transforms.

---

## Features
- Interpolates between consecutive binary slices in a TIFF stack.
- Supports two interpolation methods:
  - `perimeter` – preserves edges and holes using perimeter-based signed distance transform.
  - `area` – smooths shapes by interpolating the filled area.
- Saves interpolated slices as PNGs in a specified output folder.
- Debug visualizations of intermediate slices are optional.

---

## Installation
Clone or download the repository:

```bash
git clone https://github.com/<username>/binary-tiff-stack-interpolator.git
```
Requires MATLAB with the Image Processing Toolbox™.

## Usage

 - Place your TIFF stack in the same folder or update the inputFile path.
 - Set parameters at the top of interpolate_stack.m:
```matlab
N = 19;                        % Number of interpolation steps between slices
inputFile = 'my_stack.tif';    % Input TIFF stack
outputFolder = 'stackout';     % Folder to save output PNGs
interpMethod = 'perimeter';    % 'perimeter' or 'area'
showFigures = false;           % Show debug visualizations
```
- Run the script in MATLAB:
```matlab
interpolate_stack()
```

## Citation

If this work facilitated your research, please cite:

**Martin P.J. Ryan, et al.**  
*"Computational fluid dynamics simulation of blood flow through a retinal capillary model generated from 3D electron microscopy images"*  
DOI: TBD  

This interpolation tool was used to generate the 3D image stacks that made this research possible.



## Notes
- The recommended `perimeter` method preserves high-fidelity boundaries, which is critical for CFD simulations. The `area` method is provided for other types of binary stack interpolations.
- In the original research, [FIJI](https://github.com/fiji)’s 3D Image Viewer was used to visualize stacks and export STL meshes.
- A supplementary `slices2STL.m` script is now included. It reads the binary interpolated slices from `outputFolder` and produces an isosurface STL mesh. Run it in MATLAB with:
```matlab
slices2STL('stackout', 'output_mesh.stl', 0.5)
```
- The third parameter is the isosurface threshold (default 0.5).
