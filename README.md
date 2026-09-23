# FluidX3D

The fastest and most memory efficient lattice Boltzmann CFD software, running on all GPUs and CPUs via [OpenCL](https://github.com/ProjectPhysX/OpenCL-Wrapper "OpenCL-Wrapper"). Free for non-commercial use.

<a href="https://youtu.be/-MkRBeQkLk8"><img src="https://img.youtube.com/vi/o3TPN142HxM/maxresdefault.jpg" width="50%"></img></a><a href="https://youtu.be/1z5-ddsmAag"><img src="https://img.youtube.com/vi/1z5-ddsmAag/maxresdefault.jpg" width="50%"></img></a><br>
<a href="https://youtu.be/2BPP1oWzvi0"><img src="https://img.youtube.com/vi/2BPP1oWzvi0/maxresdefault.jpg" width="50%"></img></a><a href="https://youtu.be/K5eKxzklXDA"><img src="https://img.youtube.com/vi/K5eKxzklXDA/maxresdefault.jpg" width="50%"></img></a>
(click on images to show videos on YouTube)

<details><summary>Update History</summary>

- [v1.0](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v1.0) (04.08.2022) [changes](https://github.com/ProjectPhysX/FluidX3D/commit/768073501af725e392a4b85885009e2fa6400e48) (public release)
  - public release
- [v1.1](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v1.1) (29.09.2022) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v1.0...v1.1) (GPU voxelization)
  - added solid voxelization on GPU (slow algorithm)
  - added tool to print current camera position (key <kbd>G</kbd>)
  - minor bug fix (workaround for Intel iGPU driver bug with triangle rendering)
- [v1.2](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v1.2) (24.10.2022) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v1.1...v1.2) (force/torque computation)
  - added functions to compute force/torque on objects
  - added function to translate Mesh
  - added Stokes drag validation setup
- [v1.3](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v1.3) (10.11.2022) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v1.2...v1.3) (minor bug fixes)
  - added unit conversion functions for torque
  - `FORCE_FIELD` and `VOLUME_FORCE` can now be used independently
  - minor bug fix (workaround for AMD legacy driver bug with binary number literals)
- [v1.4](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v1.4) (14.12.2022) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v1.3...v1.4) (Linux graphics)
  - complete rewrite of C++ graphics library to minimize API dependencies
  - added interactive graphics mode on Linux with X11
  - fixed streamline visualization bug in 2D
- [v2.0](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.0) (09.01.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v1.4...v2.0) (multi-GPU upgrade)
  - added (cross-vendor) multi-GPU support on a single node (PC/laptop/server)
- [v2.1](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.1) (15.01.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.0...v2.1) (fast voxelization)
  - made solid voxelization on GPU lightning fast (new algorithm, from minutes to milliseconds)
- [v2.2](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.0) (20.01.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.1...v2.2) (velocity voxelization)
  - added option to voxelize moving/rotating geometry on GPU, with automatic velocity initialization for each grid point based on center of rotation, linear velocity and rotational velocity
  - cells that are converted from solid->fluid during re-voxelization now have their DDFs properly initialized
  - added option to not auto-scale mesh during `read_stl(...)`, with negative `size` parameter
  - added kernel for solid boundary rendering with marching-cubes
- [v2.3](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.3) (30.01.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.2...v2.3) (particles)
  - added particles with immersed-boundary method (either passive or 2-way-coupled, only supported with single-GPU)
  - minor optimization to GPU voxelization algorithm (workgroup threads outside mesh bounding-box return after ray-mesh intersections have been found)
  - displayed GPU memory allocation size is now fully accurate
  - fixed bug in `write_line()` function in `src/utilities.hpp`
  - removed `.exe` file extension for Linux/macOS
- [v2.4](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.4) (11.03.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.3...v2.4) (UI improvements)
  - added a help menu with key <kbd>H</kbd> that shows keyboard/mouse controls, visualization settings and simulation stats
  - improvements to keyboard/mouse control (<kbd>+</kbd>/<kbd>-</kbd> for zoom, <kbd>mouseclick</kbd> frees/locks cursor)
  - added suggestion of largest possible grid resolution if resolution is set larger than memory allows
  - minor optimizations in multi-GPU communication (insignificant performance difference)
  - fixed bug in temperature equilibrium function for temperature extension
  - fixed erroneous double literal for Intel iGPUs in skybox color functions
  - fixed bug in make.sh where multi-GPU device IDs would not get forwarded to the executable
  - minor bug fixes in graphics engine (free cursor not centered during rotation, labels in VR mode)
  - fixed bug in `LBM::voxelize_stl()` size parameter standard initialization
- [v2.5](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.5) (11.04.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.4...v2.5) (raytracing overhaul)
  - implemented light absorption in fluid for raytracing graphics (no performance impact)
  - improved raytracing framerate when camera is inside fluid
  - fixed skybox pole flickering artifacts
  - fixed bug where moving objects during re-voxelization would leave an erroneous trail of solid grid cells behind
- [v2.6](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.6) (16.04.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.5...v2.6) (Intel Arc patch)
  - patched OpenCL issues of Intel Arc GPUs: now VRAM allocations >4GB are possible and correct VRAM capacity is reported
- [v2.7](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.7) (29.05.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.6...v2.7) (visualization upgrade)
  - added slice visualization (key <kbd>2</kbd> / key <kbd>3</kbd> modes, then switch through slice modes with key <kbd>T</kbd>, move slice with keys <kbd>Q</kbd>/<kbd>E</kbd>)
  - made flag wireframe / solid surface visualization kernels toggleable with key <kbd>1</kbd>
  - added surface pressure visualization (key <kbd>1</kbd> when `FORCE_FIELD` is enabled and `lbm.calculate_force_on_boundaries();` is called)
  - added binary `.vtk` export function for meshes with `lbm.write_mesh_to_vtk(Mesh* mesh);`
  - added `time_step_multiplicator` for `integrate_particles()` function in `PARTICLES` extension
  - made correction of wrong memory reporting on Intel Arc more robust
  - fixed bug in `write_file()` template functions
  - reverted back to separate `cl::Context` for each OpenCL device, as the shared Context otherwise would allocate extra VRAM on all other unused Nvidia GPUs
  - removed Debug and x86 configurations from Visual Studio solution file (one less complication for compiling)
  - fixed bug that particles could get too close to walls and get stuck, or leave the fluid phase (added boundary force)
- [v2.8](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.8) (24.06.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.7...v2.8) (documentation + polish)
  - finally added more [documentation](DOCUMENTATION.md)
  - cleaned up all sample setups in `setup.cpp` for more beginner-friendliness, and added required extensions in `defines.hpp` as comments to all setups
  - improved loading of composite `.stl` geometries, by adding an option to omit automatic mesh repositioning, added more functionality to `Mesh` struct in `utilities.hpp`
  - added `uint3 resolution(float3 box_aspect_ratio, uint memory)` function to compute simulation box resolution based on box aspect ratio and VRAM occupation in MB
  - added `bool lbm.graphics.next_frame(...)` function to export images for a specified video length in the `main_setup` compute loop
  - added `VIS_...` macros to ease setting visualization modes in headless graphics mode in `lbm.graphics.visualization_modes`
  - simulation box dimensions are now automatically made equally divisible by domains for multi-GPU simulations
  - fixed Info/Warning/Error message formatting for loading files and made Info/Warning/Error message labels colored
  - added Ahmed body setup as an example on how body forces and drag coefficient are computed
  - added Cessna 172 and Bell 222 setups to showcase loading composite .stl geometries and revoxelization of moving parts
  - added optional semi-transparent rendering mode (`#define GRAPHICS_TRANSPARENCY 0.7f` in `defines.hpp`)
  - fixed flickering of streamline visualization in interactive graphics
  - improved smooth positioning of streamlines in slice mode
  - fixed bug where `mass` and `massex` in `SURFACE` extension were also allocated in CPU RAM (not required)
  - fixed bug in Q-criterion rendering of halo data in multi-GPU mode, reduced gap width between domains
  - removed shared memory optimization from mesh voxelization kernel, as it crashes on Nvidia GPUs with new GPU drivers and is incompatible with old OpenCL 1.0 GPUs
  - fixed raytracing attenuation color when no surface is at the simulation box walls with periodic boundaries
- [v2.9](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.9) (31.07.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.8...v2.9) (multithreading)
  - added cross-platform `parallel_for` implementation in `utilities.hpp` using `std::threads`
  - significantly (>4x) faster simulation startup with multithreaded geometry initialization and sanity checks
  - faster `calculate_force_on_object()` and `calculate_torque_on_object()` functions with multithreading
  - added total runtime and LBM runtime to `lbm.write_status()`
  - fixed bug in voxelization ray direction for re-voxelizing rotating objects
  - fixed bug in `Mesh::get_bounding_box_size()`
  - fixed bug in `print_message()` function in `utilities.hpp`
- [v2.10](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.10) (05.11.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.9...v2.10) (frustum culling)
  - improved rasterization performance via frustum culling when only part of the simulation box is visible
  - improved switching between centered/free camera mode
  - refactored OpenCL rendering library
  - unit conversion factors are now automatically printed in console when `units.set_m_kg_s(...)` is used
  - faster startup time for FluidX3D benchmark
  - miner bug fix in `voxelize_mesh(...)` kernel
  - fixed bug in `shading(...)`
  - replaced slow (in multithreading) `std::rand()` function with standard C99 LCG
  - more robust correction of wrong VRAM capacity reporting on Intel Arc GPUs
  - fixed some minor compiler warnings
- [v2.11](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.11) (07.12.2023) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.10...v2.11) (improved Linux graphics)
  - interactive graphics on Linux are now in fullscreen mode too, fully matching Windows
  - made CPU/GPU buffer initialization significantly faster with `std::fill` and `enqueueFillBuffer` (overall ~8% faster simulation startup)
  - added operating system info to OpenCL device driver version printout
  - fixed flickering with frustum culling at very small field of view
  - fixed bug where rendered/exported frame was not updated when `visualization_modes` changed
- [v2.12](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.12) (18.01.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.11...v2.12) (faster startup)
  - ~3x faster source code compiling on Linux using multiple CPU cores if [`make`](https://www.gnu.org/software/make/) is installed
  - significantly faster simulation initialization (~40% single-GPU, ~15% multi-GPU)
  - minor bug fix in `Memory_Container::reset()` function
- [v2.13](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.13) (11.02.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.12...v2.13) (improved .vtk export)
  - data in exported `.vtk` files is now automatically converted to SI units
  - ~2x faster `.vtk` export with multithreading
  - added unit conversion functions for `TEMPERATURE` extension
  - fixed graphical artifacts with axis-aligned camera in raytracing
  - fixed `get_exe_path()` for macOS
  - fixed X11 multi-monitor issues on Linux
  - workaround for Nvidia driver bug: `enqueueFillBuffer` is broken for large buffers on Nvidia GPUs
  - fixed slow numeric drift issues caused by `-cl-fast-relaxed-math`
  - fixed wrong Maximum Allocation Size reporting in `LBM::write_status()`
  - fixed missing scaling of coordinates to SI units in `LBM::write_mesh_to_vtk()`
- [v2.14](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.14) (03.03.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.13...v2.14) (visualization upgrade)
  - coloring can now be switched between velocity/density/temperature with key <kbd>Z</kbd>
  - uniform improved color palettes for velocity/density/temperature visualization
  - color scale with automatic unit conversion can now be shown with key <kbd>H</kbd>
  - slice mode for field visualization now draws fully filled-in slices instead of only lines for velocity vectors
  - shading in `VIS_FLAG_SURFACE` and `VIS_PHI_RASTERIZE` modes is smoother now
  - `make.sh` now automatically detects operating system and X11 support on Linux and only runs FluidX3D if last compilation was successful
  - fixed compiler warnings on Android
  - fixed `make.sh` failing on some systems due to nonstandard interpreter path
  - fixed that `make` would not compile with multiple cores on some systems
- [v2.15](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.15) (09.04.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.14...v2.15) (framerate boost)
  - eliminated one frame memory copy and one clear frame operation in rendering chain, for 20-70% higher framerate on both Windows and Linux
  - enabled `g++` compiler optimizations for faster startup and higher rendering framerate
  - fixed bug in multithreaded sanity checks
  - fixed wrong unit conversion for thermal expansion coefficient
  - fixed density to pressure conversion in LBM units
  - fixed bug that raytracing kernel could lock up simulation
  - fixed minor visual artifacts with raytracing
  - fixed that console sometimes was not cleared before `INTERACTIVE_GRAPHICS_ASCII` rendering starts
- [v2.16](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.16) (02.05.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.15...v2.16) (bug fixes)
  - simplified 10% faster marching-cubes implementation with 1D interpolation on edges instead of 3D interpolation, allowing to get rid of edge table
  - added faster, simplified marching-cubes variant for solid surface rendering where edges are always halfway between grid cells
  - refactoring in OpenCL rendering kernels
  - fixed that voxelization failed in Intel OpenCL CPU Runtime due to array out-of-bounds access
  - fixed that voxelization did not always produce binary identical results in multi-GPU compared to single-GPU
  - fixed that velocity voxelization failed for free surface simulations
  - fixed terrible performance on ARM GPUs by macro-replacing fused-multiply-add (`fma`) with `a*b+c`
  - fixed that <kbd>Y</kbd>/<kbd>Z</kbd> keys were incorrect for `QWERTY` keyboard layout in Linux
  - fixed that free camera movement speed in help overlay was not updated in stationary image when scrolling
  - fixed that cursor would sometimes flicker when scrolling on trackpads with Linux-X11 interactive graphics
  - fixed flickering of interactive rendering with multi-GPU when camera is not moved
  - fixed missing `XInitThreads()` call that could crash Linux interactive graphics on some systems
  - fixed z-fighting between `graphics_rasterize_phi()` and `graphics_flags_mc()` kernels
- [v2.17](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.17) (05.06.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.16...v2.17) (unlimited domain resolution)
  - domains are no longer limited to 4.29 billion (2³², 1624³) grid cells or 225 GB memory; if more are used, the OpenCL code will automatically compile with 64-bit indexing
  - new, faster raytracing-based field visualization for single-GPU simulations
  - added [GPU Driver and OpenCL Runtime installation instructions](DOCUMENTATION.md#0-install-gpu-drivers-and-opencl-runtime) to documentation
  - refactored `INTERACTIVE_GRAPHICS_ASCII`
  - fixed memory leak in destructors of `floatN`, `floatNxN`, `doubleN`, `doubleNxN` (all unused)
  - made camera movement/rotation/zoom behavior independent of framerate
  - fixed that `smart_device_selection()` would print a wrong warning if device reports 0 MHz clock speed
- [v2.18](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.18) (21.07.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.17...v2.18) (more bug fixes)
  - added support for high refresh rate monitors on Linux
  - more compact OpenCL Runtime installation scripts in Documentation
  - driver/runtime installation instructions will now be printed to console if no OpenCL devices are available
  - added domain information to `LBM::write_status()`
  - added `LBM::index` function for `uint3` input parameter
  - fixed that very large simulations sometimes wouldn't render properly by increasing maximum render distance from 10k to 2.1M
  - fixed mouse input stuttering at high screen refresh rate on Linux
  - fixed graphical artifacts in free surface raytracing on Intel CPU Runtime for OpenCL
  - fixed runtime estimation printed in console for setups with multiple `lbm.run(...)` calls
  - fixed density oscillations in sample setups (too large `lbm_u`)
  - fixed minor graphical artifacts in `raytrace_phi()`
  - fixed minor graphical artifacts in `ray_grid_traverse_sum()`
  - fixed wrong printed time step count on raindrop sample setup
- [v2.19](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v2.19) (07.09.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.18...v2.19) (camera splines)
  - the camera can now fly along a smooth path through a list of provided keyframe camera placements, [using Catmull-Rom splines](https://github.com/ProjectPhysX/FluidX3D/blob/master/DOCUMENTATION.md#video-rendering)
  - more accurate remaining runtime estimation that includes time spent on rendering
  - enabled FP16S memory compression by default
  - printed camera placement using key <kbd>G</kbd> is now formatted for easier copy/paste
  - added benchmark chart in Readme using mermaid gantt chart
  - placed memory allocation info during simulation startup at better location
  - fixed threading conflict between `INTERACTIVE_GRAPHICS` and `lbm.graphics.write_frame();`
  - fixed maximum buffer allocation size limit for AMD GPUs and in Intel CPU Runtime for OpenCL
  - fixed wrong `Re<Re_max` info printout for 2D simulations
  - minor fix in `bandwidth_bytes_per_cell_device()`
- [v3.0](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.0) (16.11.2024) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v2.19...v3.0) (larger CPU/iGPU simulations)
  - reduced memory footprint on CPUs and iGPU from 72 to 55 Bytes/cell (fused OpenCL host+device buffers for `rho`/`u`/`flags`), allowing 31% higher resolution in the same RAM capacity
  - faster hardware-supported and faster fallback emulation atomic floating-point addition for `PARTICLES` extension
  - hardened `calculate_f_eq()` against bad user input for `D2Q9`
  - fixed velocity voxelization for overlapping geometry with different velocity
  - fixed Remaining Time printout during paused simulation
  - fixed CPU/GPU memory printout for CPU/iGPU simulations
- [v3.1](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.1) (08.02.2025) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.0...v3.1) (more bug fixes)
  - faster `enqueueReadBuffer()` on modern CPUs with 64-Byte-aligned `host_buffer`
  - hardened ray intersection functions against planar ray edge case
  - updated OpenCL headers
  - better OpenCL device specs detection using vendor ID and Nvidia compute capability
  - better VRAM capacity reporting correction for Intel dGPUs
  - improved styling of performance mermaid gantt chart in Readme
  - added multi-GPU performance mermaid gantt chart in Readme
  - updated driver install guides
  - fixed voxelization being broken on some GPUs
  - added workaround for compiler bug in Intel CPU Runtime for OpenCL that causes Q-criterion isosurface rendering corruption
  - fixed TFlops estimate for Intel Battlemage GPUs
  - fixed wrong device name reporting for AMD GPUs
- [v3.2](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.2) (09.03.2025) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.1...v3.2) (fast force/torque summation)
  - implemented GPU-accelerated force/torque summation (~20x faster than CPU-multithreaded implementation before)
  - simplified calculating object force/torque in setups
  - improved coloring in `VIS_FIELD`/`ray_grid_traverse_sum()`
  - updated OpenCL-Wrapper now compiles OpenCL C code with `-cl-std=CL3.0` if available
  - fixed compiling on macOS with new OpenCL headers
- [v3.3](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.3) (17.05.2025) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.2...v3.3) (faster .vtk export)
  - `.vtk` export now converts and writes data in chunks, to reduce memory footprint and time for large memory allocation
  - `.vtk` files now contain original file name as metadata in title
  - `INTERACTIVE_GRAPHICS_ASCII` now renders in 2x vertical resolution but less colors
  - updated OpenCL-Wrapper: more robust dp4a detection, fixed core count reporting for RDNA4 GPUs
  - fixed `update_moving_boundaries()` kernel not being called with flags other than `TYPE_S`
  - fixed corrupted first frame until resizing with `INTERACTIVE_GRAPHICS_ASCII`
  - fixed `resolution()` function for D2Q9
  - fixed missing `<chrono>` header on some compilers
  - fixed bug in `split_regex()`
  - fixed compiler warning with `min_int`
- [v3.4](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.4) (02.07.2025) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.3...v3.4) (bug fixes)
  - updated OpenCL driver install versions
  - minor refactoring in `stream_collide()`
  - fixed bug in insertion-sort in `voxelize_mesh()` kernel causing crash on AMD GPUs
  - fixed bug in `voxelize_mesh_on_device()` host code causing initialization corruption on AMD GPUs
  - fixed dual CU and IPC reporting on AMD RDNA 1-4 GPUs
- [v3.5](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.5) (01.10.2025) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.4...v3.5) (multi-GPU particles)
  - `PARTICLES` extension now also works with multi-GPU
  - faster force spreading if volume force is axis-aligned
  - added more documentation for boundary conditions
  - updated FAQs
  - improved "hydraulic jump" sample setup
  - updated GPU driver install instructions
  - disabled zero-copy on ARM iGPUs because `CL_MEM_USE_HOST_PTR` is broken there
- [v3.6](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.6) (24.03.2026) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.5...v3.6) (improved macOS graphics)
  - improved `INTERACTIVE_GRAPHICS` support on macOS with XQuartz
  - added `Mesh::get_center_of_mass()` function, for easy rotation of any balanced rotor
  - made performance `mermaid` `gantt` chart in Readme properly colored
  - more robust Intel GPU core/CU detecton via `CL_DEVICE_IP_VERSION_INTEL`
  - OpenCL code refactoring
  - set `nvidia_compute_capability` only for Nvidia GPUs not Nvidia CPUs
  - fixed TFLOPs/s estimate for AMD CDNA3/4 GPUs
  - fixed Device Name and CU reporting for AMD GPUs with rusticl
- [v3.7](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.7) (14.05.2026) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.6...v3.7) (faster Q-criterion rendering)
  - up to 2x faster Q-criterion isosurface rendering on some GPUs
  - reduced assembly spaghettification by simpler condition for VR rendering and disabling loop unrolling in rasterization
  - micro-optimization in `convert_triangle/_interpolated()`
  - fixed empty kernel name and workgroup size error printout in OpenCL-Wrapper
- [v3.8](https://github.com/ProjectPhysX/FluidX3D/releases/tag/v3.8) (05.09.2026) [changes](https://github.com/ProjectPhysX/FluidX3D/compare/v3.7...v3.8) (faster rendering & fixes)
  - dispatch marching-cubes kernels only for `(Nx-1)*(Ny-1)*(Nz-1)` instead of `N`
  - made `graphics_flags_mc()` kernel up to 40% faster with local memory optimization
  - added local memory optimization also for `graphics_rasterize_phi()` kernel, small optimization in `marching_cubes()`
  - updated driver install instructions
  - fixed `graphics_q()` kernel with `GRAPHICS_LSQ=8` on older Nvidia GPUs through register optimization
  - fixed z-buffer flickering on Intel Panther Lake iGPUs
  - disabled zero-copy on Nvidia iGPUs such as GB10 because `CL_MEM_USE_HOST_PTR` is broken there
  - fixed missing `allocated_bitmap/zbuffer` in `Camera` move assignment
  - fixed missing type cast in OpenCL-Wrapper
  - fixed crash/segfault on exit
  - removed `opencl_unroll_hint` again (unsupported on some older GPUs)

</details>



## How to get started?

Read the [FluidX3D Documentation](DOCUMENTATION.md)!




### Hardware

- <details><summary>Can FluidX3D run on multiple GPUs at the same time?</summary><br>Yes. The simulation grid is then split in domains, one for each GPU (domain decomposition method). The GPUs essentially pool their memory, enabling much larger grid resolution and higher performance. Rendering is parallelized across multiple GPUs as well; each GPU renders its own domain with a 3D offset, then rendered frames from all GPUs are overlaid with their z-buffers. Communication between domains is done over PCIe, so no SLI/Crossfire/NVLink/InfinityFabric is required. All GPUs must however be installed in the same node (PC/laptop/server). Even <a href="https://youtu.be/_8Ed8ET9gBU">unholy combinations of AMD+Intel+Nvidia GPUs will work</a>, although it is recommended to only use GPUs with similar memory capacity and bandwidth together. Using a fast gaming GPU and slow integrated GPU together would only decrease performance due to communication overhead.<br><br></details>

- <details><summary>Can I run FluidX3D on the CPU?</summary><br>Yes, and this is especially useful when you need more memory than a GPU can offer. You only need to install the <a href="https://github.com/ProjectPhysX/FluidX3D/blob/master/DOCUMENTATION.md#0-install-gpu-drivers-and-opencl-runtime">Intel CPU Runtime for OpenCL</a>.<br><br></details>

- <details><summary>I'm on a budget and have only a cheap computer. Can I run FluidX3D on my toaster PC/laptop?</summary><br>Absolutely. Today even the most inexpensive hardware, like integrated GPUs or entry-level gaming GPUs, support OpenCL. You might be a bit more limited on memory capacity and grid resolution, but you should be good to go. I've tested FluidX3D on very old and inexpensive hardware and even on my Samsung S9+ smartphone, and it runs just fine, although admittedly a bit slower.<br><br></details>

- <details><summary>I don't have an expensive workstation GPU, but only a gaming GPU. Will performance suffer?</summary><br>No. Efficiency on gaming GPUs is exactly as good as on their "professional"/workstation counterparts. Performance often is even better as gaming GPUs have higher boost clocks.<br><br></details>

- <details><summary>Do I need a GPU with ECC memory?</summary><br>No. Gaming GPUs work just fine. Some Nvidia GPUs automatically reduce memory clocks for compute applications to almost entirely eliminate memory errors.<br><br></details>

- <details><summary>My GPU does not support CUDA. Can I still use FluidX3D?</summary><br>Yes. FluidX3D uses OpenCL and not CUDA, so it runs on any GPU from any vendor since around 2009.<br><br></details>

- <details><summary>I don't have a dedicated graphics card at all. Can I still run FluidX3D on my PC/laptop?</summary><br>Yes. FluidX3D also runs on all integrated GPUs since around 2012, and also on CPUs.<br><br></details>

- <details><summary>In the benchmarks you list some very expensive hardware. How do you get access to that?</summary><br>As a PhD candidate in computational physics, I used FluidX3D for my research, so I had access to BZHPC, SuperMUC-NG, JSC JURECA-DC, and Leonardo supercomputers.<br><br></details>

### Graphics

- <details><summary>I don't have an RTX/DXR GPU that supports raytracing. Can I still use raytracing graphics in FluidX3D?</summary><br>Yes, and at full performance. FluidX3D does not use a bounding volume hierarchy (BVH) to accelerate raytracing, but fast ray-grid traversal instead, implemented directly in OpenCL C. This is much faster than BVH for moving isosurfaces in the LBM grid (~N vs. ~N²+log(N) runtime; LBM itself is ~N³), and it does not require any dedicated raytracing hardware. Raytracing in FluidX3D runs on any GPU that supports OpenCL 1.2.<br><br></details>

- <details><summary>I have a datacenter/mining GPU without any video output or graphics hardware. Can FluidX3D still render simulation results?</summary><br>Yes. FluidX3D does all rendering (rasterization and raytracing) in OpenCL C, so no display output and no graphics features like OpenGL/Vulkan/DirectX are required. Rendering is just another form of compute after all. Rendered frames are passed to the CPU over PCIe and then the CPU can either draw them on screen through dedicated/integrated graphics or write them to the hard drive.<br><br></details>

- <details><summary>I'm running FluidX3D on a remote (super-)computer and only have an SSH terminal. Can I still use graphics somehow?</summary><br>Yes, either directly as interactive ASCII graphics in the terminal or by storing rendered frames on the hard drive and then copying them over via `scp -r user@server.url:"~/path/to/images/folder" .`.<br><br></details>

- <details><summary>Graphics support on Apple macOS?</summary>

  <br>On macOS and Android, [`INTERACTIVE_GRAPHICS`](src/defines.hpp) mode is not supported, as no X11 is available. You can still use [`INTERACTIVE_GRAPHICS_ASCII`](src/defines.hpp) though, or <a href="https://github.com/ProjectPhysX/FluidX3D/blob/master/DOCUMENTATION.md#video-rendering">render video</a> to the hard drive with regular [`GRAPHICS`](src/defines.hpp) mode.<br><br>

</details>

### Licensing

- <details><summary>I want to learn about programming/software/physics/engineering. Can I use FluidX3D for free?</summary><br>Yes. Anyone can use FluidX3D for free for public research, education or personal use. Use by scientists, students and hobbyists is free of charge and well encouraged.<br><br></details>

- <details><summary>I am a scientist/teacher with a paid position at a public institution. Can I use FluidX3D for my research/teaching?</summary><br>Yes, you can use FluidX3D free of charge. This is considered research/education, not commercial use. To give credit, the <a href="https://github.com/ProjectPhysX/FluidX3D#references">references</a> listed below should be cited. If you publish data/results generated by altered source versions, the altered source code must be published as well.<br><br></details>

- <details><summary>I work at a company in CFD/consulting/R&D or related fields. Can I use FluidX3D commercially?</summary><br>No. Commercial use is not allowed with the current license.<br><br></details>

- <details><summary>Is FluidX3D open-source?</summary><br>No. "Open-source" as a technical term is defined as freely available without any restriction on use, but I am not comfortable with that. I have written FluidX3D in my spare time and no one should milk it for profits while I remain uncompensated, especially considering what other CFD software sells for. The technical term for the type of license I choose is "source-available no-cost non-commercial". The source code is freely available, and you are free to use, to alter and to redistribute it, as long as you do not sell it or make a profit from derived products/services, and as long as you do not use it for any military purposes (see the <a href="https://github.com/ProjectPhysX/FluidX3D/blob/master/LICENSE.md">license</a> for details).<br><br></details>

- <details><summary>Will FluidX3D at some point be available with a commercial license?</summary><br>Maybe I will add the option for a second, commercial license later on. If you are interested in commercial use, let me know. For non-commercial use in science and education, FluidX3D is and will always be free.<br><br></details>



## External Code/Libraries/Images used in FluidX3D

- [OpenCL-Headers](https://github.com/KhronosGroup/OpenCL-Headers) and [C++ Wrapper](https://github.com/KhronosGroup/OpenCL-CLHPP) for GPU parallelization ([Khronos Group](https://www.khronos.org/opencl/))
- [Win32 API](https://learn.microsoft.com/en-us/windows/win32/api/winbase/) for interactive graphics in Windows ([Microsoft](https://www.microsoft.com/))
- [X11/Xlib](https://www.x.org/releases/current/doc/libX11/libX11/libX11.html) for interactive graphics in Linux ([The Open Group](https://www.x.org/releases/current/doc/libX11/libX11/libX11.html))
- [marching-cubes tables](http://paulbourke.net/geometry/polygonise/) for isosurface generation on GPU ([Paul Bourke](http://paulbourke.net/geometry/))
- [`src/lodepng.cpp`](https://github.com/lvandeve/lodepng/blob/master/lodepng.cpp) and [`src/lodepng.hpp`](https://github.com/lvandeve/lodepng/blob/master/lodepng.h) for `.png` encoding and decoding ([Lode Vandevenne](https://lodev.org/))
- [SimplexNoise](https://weber.itn.liu.se/~stegu/simplexnoise/SimplexNoise.java) class in [`src/utilities.hpp`](https://github.com/ProjectPhysX/FluidX3D/blob/master/src/utilities.hpp) for generating continuous noise in 2D/3D/4D space ([Stefan Gustavson](https://github.com/stegu))
- [`skybox/skybox8k.png`](https://www.hdri-hub.com/hdri-skies-aviation-aerospace) for free surface raytracing ([HDRI Hub](https://www.hdri-hub.com/))



## References

- Lehmann, M.: [Computational study of microplastic transport at the water-air interface with a memory-optimized lattice Boltzmann method](https://doi.org/10.15495/EPub_UBT_00006977). PhD thesis, (2023)
- Lehmann, M.: [Esoteric Pull and Esoteric Push: Two Simple In-Place Streaming Schemes for the Lattice Boltzmann Method on GPUs](https://doi.org/10.3390/computation10060092). Computation, 10, 92, (2022)
- Lehmann, M., Krause, M., Amati, G., Sega, M., Harting, J. and Gekle, S.: [Accuracy and performance of the lattice Boltzmann method with 64-bit, 32-bit, and customized 16-bit number formats](https://www.researchgate.net/publication/362275548_Accuracy_and_performance_of_the_lattice_Boltzmann_method_with_64-bit_32-bit_and_customized_16-bit_number_formats). Phys. Rev. E 106, 015308, (2022)
- Lehmann, M.: [Combined scientific CFD simulation and interactive raytracing with OpenCL](https://www.researchgate.net/publication/360501260_Combined_scientific_CFD_simulation_and_interactive_raytracing_with_OpenCL). IWOCL'22: International Workshop on OpenCL, 3, 1-2, (2022)
- Lehmann, M., Oehlschlägel, L.M., Häusl, F., Held, A. and Gekle, S.: [Ejection of marine microplastics by raindrops: a computational and experimental study](https://doi.org/10.1186/s43591-021-00018-8). Micropl.&Nanopl. 1, 18, (2021)
- Lehmann, M.: [High Performance Free Surface LBM on GPUs](https://doi.org/10.15495/EPub_UBT_00005400). Master's thesis, (2019)
- Lehmann, M. and Gekle, S.: [Analytic Solution to the Piecewise Linear Interface Construction Problem and Its Application in Curvature Calculation for Volume-of-Fluid Simulation Codes](https://doi.org/10.3390/computation10020021). Computation, 10, 21, (2022)



