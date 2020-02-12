Modelling Natural Convection with FreeFem++
=================================================

Natural convection is a heat transfer process that is present in our everyday life: from the cooling of little electronic devices, to indoor climate systems, to environmental transport problems. In this set of codes, a finite element method is implemented for the solution of the equations of conservation of mass, momentum and energy, coupled by the boussinesq approximation.

## Main Characteristics

* The method can handle a temperature-dependent viscosity and a tensorial,
space-dependent thermal conductivity.

* Convergence for the method has only been theoretically proved for two-dimensional domains (see next section for the three-dimensional case).

* The implementation is based on [FreeFem++](https://freefem.org/). 

* The method is of mixed nature. As such, it computes approximations for the pseudostress tensor, velocity, vorticity, temperature and normal heat flux through the boundary. Quantities such as pressure are postprocessed using the computed variables.

* For a first order method, the following combination of finite elements can be used:
```C++
fespace Hhs(Th,[RT0,RT0]); 	// Pseudostress
fespace Hhu(Th,[P1,P1]); 	// Velocity
fespace Hhg(Th,P0);			// Vorticity
fespace Hhp(Th,P1);			// Temperature
fespace Hhl(Sh,P0edge);		// Normal heat flux through the boundary
```
* For a second order method, use
```C++
fespace Hhs(Th,[RT1,RT1]); 	// Pseudostress
fespace Hhu(Th,[P2,P2]); 	// Velocity
fespace Hhg(Th,P1dc);			// Vorticity
fespace Hhp(Th,P1);			// Temperature
fespace Hhl(Sh,P1edge);		// Normal heat flux through the boundary
```
This requires to load "Element_Mixte" and "Element_PkEdge".

* Higher order finite elements can also be used, however, the computational cost of this method might then become prohibitive.

* Graphics can be exported in VTK format (Paraview).

* Data such as DOFs, errors and rates of convergence can be exported in .m format (Matlab).

## Reference article

To find out more about the theoretical aspects of this method, as well as comparisons between the codes in this repository and their expected results, read

> J. A. Almonacid, G. N. Gatica and R. Oyarzua, 
> [*A mixed-primal finite element method for the Boussinesq problem with temperature-dependent viscosity*](https://rdcu.be/32pk). 
> Calcolo 55 (2018), no. 3, Art. 36, 42 pp.
