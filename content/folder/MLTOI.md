> this project is: **in progress**

stands for: *Machine-Learning-Enabled Topological Order Identification*

abstract: skyrmions (pronounced skur-mee-ons) are tiny swirling magnetic structures formed by electron spin. their topology makes them stable and energy efficient which makes them promising for next-gen memory devices and spintronics computing. this project focuses on using ml to anaylze both ferromagnetic and antiferromagnetic materials to predict skyrmion formation and identify phase transitions. 

<div align="center" style="font-size: 1.3rem;"> * * * </div>
resources used: Siesta, materialsproject, pseudodojo, TB2J

at the current stage of the project, we are still running calculations for DFT and materials magnetic interactions using Siesta and TB2J. we do this feeding FDF files (which we are in the process of making) into Siesta and taking the electronic structure results to input into TB2J. 

currently:
- finding method to automate FDF file generation
- finding method to obtain pseudopotential for actinides (idfk this is impossible)

Example of FDF (Iron)
```
SystemName	siesta
SystemLabel	siesta

SaveHS	True
CDF.Save	True

MaxSCFIteration	60
SCF.DM.Tolerance	0.0001
SCF.EDM.Tolerance	1e-2 eV
SCF.H.Tolerance	1e-3 eV
SCF.Mixer.History	6
SCF.Mixer.Method	Pulay
SCF.Mixer.Weight	0.3
SCF.Mix.Spin sum

SCFMustConverge	True

Spin     	COLLINEAR
XC.functional	GGA
XC.authors	PBE

MeshCutoff	600 Ry

NumberOfSpecies	1
NumberOfAtoms	1
%block ChemicalSpecieslabel
    1 26 Fe
%endblock ChemicalSpecieslabel


## Psml version
#PAO.EnergyShift	0.1	eV
#%block PAO.BasisSizes
#    Fe  DZP
#%endblock PAO.BasisSizes



## master version
%block PAO.Basis                 # Define Basis set
Fe                    4                    # Species label, number of l-shells
 n=3   0   1                         # n, l, Nzeta
   2.906
   1.000
 n=4   0   2 P   1                   # n, l, Nzeta, Polarization, NzetaPol
   8.731      5.926
   1.000      1.000
 n=3   1   1                         # n, l, Nzeta
   3.293
   1.000
 n=3   2   2                         # n, l, Nzeta
   5.853      2.263
   1.000      1.000
%endblock PAO.Basis



LatticeConstant	1.0 Ang
%block LatticeVectors
    2.466540770000000     0.000000000000000     0.000000000000000 
    -0.822180256484402     2.325476939451225     0.000000000000000 
    -0.822180256484402     -1.162738469338971     2.013922105702875 
%endblock LatticeVectors


AtomicCoordinatesFormat  Ang
%block AtomicCoordinatesAndAtomicSpecies
     0.000000000      0.000000000      0.000000000 1
%endblock AtomicCoordinatesAndAtomicSpecies

%block DM.InitSpin
    1 2.30000000000000
%endblock DM.InitSpin

DM.UseSaveDM	False

#KPoint grid
%block kgrid_Monkhorst_Pack
     7       0       0  0.0
     0       7       0  0.0
     0       0       7  0.0
%endblock kgrid_Monkhorst_Pack
```

**TB2J**:
orbitals used in decomposition: 
```
Fe1 : ('3s', '4s', '3py', '3pz', '3px', '4py', '4pz', '4px', '3dxy', '3dyz', '3dz2', '3dxz', '3dx2-y2')
```

**Output:** exchange pair, R lattice vector, isotropic heisenberg exchange parameter, vector, distance
```
Exchange: 
    i      j          R        J_iso(meV)          vector          distance(A) 
----------------------------------------------------------------------------------------
   Fe1   Fe1   ( -1,   0,   0) 17.5071   (-2.467,  0.000,  0.000)  2.467 
J_iso: 17.5071 
```