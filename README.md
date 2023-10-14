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
* Finaly, we will add an additional branch with R2 to trim $V_{BG}$ voltage so that $V_{BG} = V_{CTAT} + \alpha*V_{PTAT} = V_{BE3} + (kT/q)*TC$,   where $TC = (R2/R1)ln(N)$
* Current calculated as $I_0 = (kT/q)*(1/R_1)*ln(N)$ and will be determined from simulations
  ****
  
## Design & Simulations
Initial Design - 

At first we will choose R1 to target for $I_0=10[uA]$ -> based on simulations $R_1 = 5.4[KOhm]$ - 
<img width="500" height="500" alt="image" align=center src="https://github.com/dsapir4422/BGAP-cell-with-feedback/assets/87266625/fc5ffbaa-cd19-40c2-ade7-5378ce13d772">

We will also simulate CTAT and PTAT voltage behavior over temperatures - 
![image](https://github.com/dsapir4422/BGAP-cell-with-feedback/assets/87266625/d04fb36c-a9bd-4d2c-9846-57ea3f4bf4c5)

Now, in order to determine R2 value, we will simulate the ratio of CTAT/PTAT slope -  $\delta V_{BG}/ \delta Temp = R_2/R_1$ - 
<img width="383" alt="image" src="https://github.com/dsapir4422/BGAP-cell-with-feedback/assets/87266625/8e9987fd-eb94-4bca-8233-b12f3047d0b5">

=> $R_2 = R_1 * 10.8 = 58.3[Kohm]$ => $TC = (R2/R1)ln(8) = 22.45$.  from simulation - $V_{BE3} = 583[mV]$, which gives us a BG value of  $V_{BG}= V_{BE3} + (kT/q)*TC = 1.17[V]$

re-simulating VREF, PTAT, and CTAT - 

<img width="800" height="500" alt="image" align=left src="https://github.com/dsapir4422/BGAP-cell-with-feedback/assets/87266625/56c7bd88-ea55-4294-b9e0-d2fa2fce9346">

