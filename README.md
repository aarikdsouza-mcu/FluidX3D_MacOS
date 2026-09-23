# FluidX3D

The fastest and most memory efficient lattice Boltzmann CFD software, running on all GPUs and CPUs via [OpenCL](https://github.com/ProjectPhysX/OpenCL-Wrapper "OpenCL-Wrapper"). Free for non-commercial use.

## How to get started?

Read the [FluidX3D Documentation](DOCUMENTATION.md)!



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



