# BGAP-cell-with-feedback
In this project we will show the design of a Band Gap (BGAP) circuit with negative feedback to reduce current mismatch and beta dependency.

We will use CMOS general pdk 90nm (gpdk90) technology by Cadence.

**Specifications**
* $V_{BG} \approx 1.2[V]$
* $V_{AA} = 1.8[V]$
* $I_0 = 10[uA]$

The specifications will hold cross PVT corners: process - TT,SS,FF,FS,SF, Temperatures ranging (-20,80) and +/- 10% supply change.

## Design topology & calculations
We will design the below circuit - 

<img width="400" height="400" alt="image" align=left src="https://github.com/dsapir4422/BGAP-cell-with-feedback/assets/87266625/6b9c35a2-698b-4b8e-8e53-d6bef036a849">

**Circuit explained**
* The voltage on the diode of left most branch is CTAT and defined as $V_{CTAT} = V_{BE} = (kT/q)ln(I_c/I_s)$
* The voltage on R1 is PTAT and defined as $V_{PTAT} = \Delta V_{BE} = (kT/q)ln(N)$
* N = number of diodes, we will use 8 for Layout symmetry of 9 diodes (8 on R1 branch and 1 on CTAT branch)
* We will use an ideal VCCS (opamp) to provide negative feedback for the circuit, this in order for both currents on CTAT and PTAT branches to be equal.
* Finaly, we will add an additional branch with R2 to trim $V_{BG}$ voltage so that $V_{BG} = V_{CTAT} + \alpha*V_{PTAT} = V_{BE3} + (kT/q)*NC$,   where $NC = (R2/R1)ln(N)$
* Current calculated as $I_0 = (kT/q)*(1/R_1)*ln(N)$ and will be determined from simulations

# Design & Simulations
Initial Design - 

<img width="500" height="500" alt="image" align=left src="https://github.com/dsapir4422/BGAP-cell-with-feedback/assets/87266625/fc5ffbaa-cd19-40c2-ade7-5378ce13d772">


