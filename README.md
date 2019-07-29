# Thickened Flame Module
This module was developed by [ATA Engineering](http://www.ata-e.com) as an 
add-on to the Loci/CHEM computational fluid dynamics (CFD) solver. The module 
implements the thickened flame model as a combustion model. The module 
artificially thickens the flame so that it can be resolved on a coarser grid.
The flame thickening occurs by modifying the diffusion and reaction source 
terms in the species transport equations. Thickening the flame reduces its
sensitivity to turbulent fluctuations. These combustion-turbulence interactions
are modeled with an efficiency function that further modifies the diffusion 
and reaction source terms in the species transport equations.

# Dependencies
This module depends on both Loci and CHEM being installed. Loci is an open
source framework developed at Mississippi State University (MSU) by Dr. Ed 
Luke. The framework provides a rule-based programming model and can take 
advantage of massively parallel high performance computing systems. CHEM is a 
full featured open source CFD code with finite-rate chemistry built on the Loci 
framework. CHEM is export controlled under the International Traffic In Arms 
Regulations (ITAR). Both Loci and CHEM can be obtained from the 
[SimSys Software Forum](http://www.simcenter.msstate.edu) hosted by MSU.

# Installation Instructions
First Loci and CHEM should be installed. The **LOCI_BASE** environment
variable should be set to point to the Loci installation directory. The 
**CHEM_BASE** environment variable should be set to point to the CHEM 
installation directory. The installation process follows the standard 
make, make install procedure.

```bash
make
make install
```

# Usage
First the module must be loaded at the top of the **vars** file. 
The user can then specify the relevant thicked flame parameters within the
**thickenedFlame** options list. The chemistry jacobian should be set through
the **tf_chemistry_jacobian** variable, and the **chemistry_jacobian** variable
should be set to **none**.

```
loadModule: thickenedFlame

thickenedFlame:<Fmax=10, pvBurnedValue=2000 K, pvUnburnedValue=300 K, 
                laminarFlameSpeed=0.1 m/s, laminarFlameThickness=0.001 m>
smoothingSteps: 14
chemistry_jacobian: none
tf_chemistry_jacobian: analytic
                
```

