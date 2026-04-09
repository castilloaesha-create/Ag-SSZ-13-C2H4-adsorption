# APPENDICES

## Computational Input Parameters for Density Functional Theory Calculations

---

## Appendix A: Computational Input Parameters

### A.1 Quantum ESPRESSO Input File Structure

All calculations were performed using Quantum ESPRESSO (QE) package. The input files follow the standard QE namelist format with the following structure:

```
&CONTROL
    calculation   = 'vc-relax' / 'scf' / 'nscf'
    outdir        = './outdir'
    pseudo_dir    = './'
    forc_conv_thr =  0.001
    etot_conv_thr =  0.0001
/

&SYSTEM
    ibrav       = 0
    ecutwfc     = 60
    ecutrho     = 240
    nat         = [number of atoms]
    ntyp        = [number of atomic types]
    occupations = 'smearing'
    smearing    = 'gaussian'
    degauss     = 0.02
/

&ELECTRONS
    conv_thr    = 1.00000e-08
/

&IONS
    ion_dynamics = 'bfgs'
/

&CELL
    cell_dofree    = 'all'
    cell_dynamics  = 'bfgs'
    press_conv_thr = 0.05
/

K_POINTS {automatic}
    [kx] [ky] [kz] [0] [0] [0]

ATOMIC_SPECIES
    [Element] [Mass] [Pseudopotential File]

ATOMIC_POSITIONS {angstrom}
    [Element] [x] [y] [z]
    ...

CELL_PARAMETERS {angstrom}
    [lattice vectors]
```

*Note: Complete input files for all systems are available in the deposited dataset (see Appendix D).*

---

### A.2 Summary of All Calculated Systems

| System ID | Description | Formula | Total Atoms | Atomic Types | Calculation Type | Input File Location |
|-----------|-------------|---------|-------------|--------------|------------------|---------------------|
| S1 | Pristine SSZ-13 (Si/Al/Ag) | SiₓAl₁Ag₁Oᵧ | 109 | 4 (Si, O, Al, Ag) | Relax | `3_VC_RELAX_SSZ_13_Al_Ag_C2H4/1_RELAX_SSZ_13_Ag_Al.in` |
| S2 | Unsubstituted SSZ-13 (Si-only) | SiₓOᵧ | 108 | 2 (Si, O) | VC-Relax | `2_VC_RELAX_no_Al_Ag/1_VC_RELAX.in` |
| S3 | Ag-SSZ-13 + 1 C₂H₄ | SiₓAl₁Ag₁Oᵧ(C₂H₄)₁ | 115 | 6 (Si, O, Al, Ag, C, H) | Relax | `3_VC_RELAX_SSZ_13_Al_Ag_C2H4/2_RELAX_SSZ_13_Ag_Al_1_C2H4.in` |
| S4 | Ag-SSZ-13 + 2 C₂H₄ | SiₓAl₁Ag₁Oᵧ(C₂H₄)₂ | 121 | 6 (Si, O, Al, Ag, C, H) | Relax | `3_VC_RELAX_SSZ_13_Al_Ag_C2H4/3_RELAX_SSZ_13_Ag_Al_2_C2H4.in` |
| S5 | Ag-SSZ-13 + 3 C₂H₄ | SiₓAl₁Ag₁Oᵧ(C₂H₄)₃ | 127 | 6 (Si, O, Al, Ag, C, H) | Relax | `3_VC_RELAX_SSZ_13_Al_Ag_C2H4/4_RELAX_SSZ_13_Ag_Al_3_C2H4.in` |
| S6 | SSZ-13 (no adsorbate, D3) | SiₓOᵧ | 108 | 2 (Si, O) | Relax | `4_VC_RELAX_SSZ_13_C2H4/1_RELAX_SSZ_13.in` |
| S7 | C₂H₄ (gas phase) | C₂H₄ | 6 | 2 (C, H) | SCF | `9_ENERGY_C2H4/1_SCF.in` |

*Note: Atomic positions provided in angstroms. Full supercell contains 108–127 atoms depending on system.*

---

### A.3 Volume-Constrained Relaxation (VC-Relax) Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Calculation Type | vc-relax / relax | Simultaneous atomic position and cell optimization |
| Exchange-Correlation Functional | PBE-DFT-D3 | Includes Grimme's D3 dispersion corrections |
| Plane-Wave Cutoff (ecutwfc) | 60 Ry | Wavefunction basis set limit |
| Charge Density Cutoff (ecutrho) | 240 Ry | Charge density basis set limit (4× ecutwfc) |
| Force Convergence Threshold | 1.0 × 10⁻³ Ry/bohr | Maximum ionic force |
| Energy Convergence Threshold | 1.0 × 10⁻⁴ Ry | Total energy change |
| Pressure Convergence Threshold | 5.0 × 10⁻² GPa | Cell stress limit |
| Ionic Dynamics | BFGS | Quasi-Newton optimization algorithm |
| Cell Dynamics | BFGS | Cell optimization algorithm |
| Cell Constraints | all | All lattice vectors allowed to vary |
| k-Point Mesh | 3 × 3 × 3 or Gamma | Monkhorst-Pack grid |
| Smearing | Gaussian, 0.02 Ry | Electronic occupation broadening |

**Systems Calculated:**
- Pristine SSZ-13 (Si/Al/Ag) – `1_RELAX_SSZ_13_Ag_Al.in`
- Unsubstituted SSZ-13 (Si-only) – `1_VC_RELAX.in`
- Ag-SSZ-13 + 1 C₂H₄ – `2_RELAX_SSZ_13_Ag_Al_1_C2H4.in`
- Ag-SSZ-13 + 2 C₂H₄ – `3_RELAX_SSZ_13_Ag_Al_2_C2H4.in`
- Ag-SSZ-13 + 3 C₂H₄ – `4_RELAX_SSZ_13_Ag_Al_3_C2H4.in`
- SSZ-13 (D3-corrected) – `1_RELAX_SSZ_13.in`

---

### A.4 Self-Consistent Field (SCF) Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Calculation Type | scf | Single-point energy calculation |
| Exchange-Correlation Functional | PBE-DFT-D3 | Same as VC-Relax (vdw_corr='dft-d3') |
| Plane-Wave Cutoff (ecutwfc) | 60 Ry | Consistent with relaxation |
| Charge Density Cutoff (ecutrho) | 240 Ry | Consistent with relaxation |
| SCF Convergence Threshold | 1.0 × 10⁻⁸ Ry | Electronic minimization |
| k-Point Mesh | 3 × 3 × 3 | Monkhorst-Pack grid |
| Smearing | Gaussian, 0.02 Ry | Electronic occupation broadening |

**Systems Calculated:**
- Ag-SSZ-13 (reference framework energy) – `7_ENERGY_SSZ_13_Ag_Al_C2H4/1_SSZ_13/1_SCF.in`
- Ag-SSZ-13 + 1 C₂H₄ – `7_ENERGY_SSZ_13_Ag_Al_C2H4/2_SSZ_13_1_C2H4/1_SCF.in`
- Ag-SSZ-13 + 2 C₂H₄ – `7_ENERGY_SSZ_13_Ag_Al_C2H4/3_SSZ_13_2_C2H4/1_SCF.in`
- Ag-SSZ-13 + 3 C₂H₄ – `7_ENERGY_SSZ_13_Ag_Al_C2H4/4_SSZ_13_3_C2H4/1_SCF.in`
- Isolated C₂H₄ molecule – `9_ENERGY_C2H4/1_SCF.in`

---

### A.5 Electron Localization Function (ELF) Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Calculation Type | nscf + pp.x (plot_num=8) | Electron localization analysis |
| Exchange-Correlation Functional | PBE-DFT-D3 | Same as SCF |
| Plane-Wave Cutoff (ecutwfc) | 60 Ry | Consistent with SCF |
| k-Point Mesh | System-dependent | See individual input files |
| Plot Type | plot_num = 8 | ELF calculation flag |
| Output Format | Cube format (output_format=6) | 3D grid data |
| Interpolation | Fourier | Reciprocal space interpolation |

**Systems Analyzed:**
- Ag-SSZ-13 (pristine framework) – `5_ELF_SSZ_13_Ag_Al_C2H4/1_SSZ_13/`
- Ag-SSZ-13 + 1 C₂H₄ – `5_ELF_SSZ_13_Ag_Al_C2H4/2_SSZ_13_1_C2H4/`
- Ag-SSZ-13 + 2 C₂H₄ – `5_ELF_SSZ_13_Ag_Al_C2H4/3_SSZ_13_2_C2H4/`
- Ag-SSZ-13 + 3 C₂H₄ – `5_ELF_SSZ_13_Ag_Al_C2H4/4_SSZ_13_3_C2H4/`

**ELF Calculation Workflow:**
1. SCF calculation (`1_SCF.in`) – Generate charge density
2. Plot generation (`2_PP_ELF.in`) – Compute ELF using `pp.x`

---

### A.6 Calculation Workflow Summary

**Step 1: Structural Optimization**
```
VC-Relax/Relax → Optimized geometry for all systems
```

**Step 2: Single-Point Energy Calculations**
```
SCF → Total energies for adsorption energy calculation
```

**Step 3: Electron Localization Analysis**
```
SCF → pp.x (plot_num=8) → ELF cube files → Visualization
```

**Adsorption Energy Calculation:**
```
E_ads = E(Ag-SSZ-13 + nC2H4) - E(Ag-SSZ-13) - n × E(C2H4)
```

where n = 1, 2, or 3 ethylene molecules

---

## Appendix B: Pseudopotential Information

### B.1 Pseudopotential Files Used

| Element | Pseudopotential File | Atomic Mass (amu) |
|---------|---------------------|-------------------|
| Si | Si.upf | 28.08550 |
| O | O.upf | 15.99940 |
| Al | Al.upf | 26.98154 |
| Ag | Ag.upf | 107.86820 |
| C | C.upf | 12.01070 |
| H | H.upf | 1.00794 |

*Note: Pseudopotentials in standard Quantum ESPRESSO UPF format. Verify pseudopotential generation method (USPP/PAW/NCPP) from your QE pseudopotential library source.*

---

## Appendix C: High-Performance Computing Job Submission Templates

### C.1 SLURM Job Script Template (Actual Configuration)

```bash
#!/bin/bash
#SBATCH --partition=batch
#SBATCH --qos=240c-1h_batch
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=40
#SBATCH --cpus-per-task=2
#SBATCH --mem=144G
#SBATCH --job-name=[JOB_NAME]
#SBATCH --output=[OUTPUT_FILE].out
#SBATCH --mail-user=[EMAIL]
#SBATCH --mail-type=ALL
#SBATCH --requeue

# Set stack size to unlimited
ulimit -s unlimited

# Start benchmarking
start_time=$(date +%s.%N)

# Print SLURM job parameters
echo "Submitted on $(date)"
echo "SLURM_JOB_ID          : ${SLURM_JOB_ID}"
echo "SLURM_JOB_NODELIST    : ${SLURM_JOB_NODELIST}"
echo "SLURM_NTASKS          : ${SLURM_NTASKS}"
echo "SLURM_MEM_PER_NODE    : ${SLURM_MEM_PER_NODE}"

# Load Quantum ESPRESSO module
module load anaconda
mamba activate qe-7.2

# Run calculation
DATADIR=/home/scratch3/Calculations
mpirun pw.x -i [INPUT_FILE].in > [OUTPUT_FILE].out

# End benchmarking
end_time=$(date +%s.%N)
echo "Finished on $(date)"
run_time=$(python -c "print($end_time - $start_time)")
echo "Total runtime (sec): ${run_time}"
```

### C.2 HPC System Specifications

| Parameter | Value |
|-----------|-------|
| Quantum ESPRESSO Version | 7.2 |
| Environment Manager | Conda (mamba) |
| Nodes per Job | 1 |
| Tasks per Node | 40 |
| CPUs per Task | 2 |
| Total Cores | 80 |
| Memory per Node | 144 GB |
| Partition | batch |
| QOS | 240c-1h_batch |

---

## Appendix D: Data Availability and Repository Information

### D.1 Deposited Dataset

All computational input files, optimized structures, and raw output data supporting this thesis are deposited in the following repository:

**Repository:** [Name, e.g., Materials Cloud / Zenodo / Institutional Repository]  
**DOI:** [To be assigned upon deposition]  
**URL:** [Direct link to collection]

### D.2 File Organization

The deposited dataset is organized as follows:

```
DOI_FOLDER/
├── 01_VC_RELAX/
│   ├── 0_JOB_SCRIPT.in
│   └── 1_VC_RELAX.in
├── 02_VC_RELAX_no_Al_Ag/
│   ├── 0_JOB_SCRIPT.in
│   └── 1_VC_RELAX.in
├── 03_VC_RELAX_SSZ_13_Al_Ag_C2H4/
│   ├── 0_JOB_SCRIPT.in
│   ├── 1_RELAX_SSZ_13_Ag_Al.in
│   ├── 2_RELAX_SSZ_13_Ag_Al_1_C2H4.in
│   ├── 3_RELAX_SSZ_13_Ag_Al_2_C2H4.in
│   ├── 4_RELAX_SSZ_13_Ag_Al_3_C2H4.in
│   └── 5_RELAX_C2H4.in
├── 04_VC_RELAX_SSZ_13_C2H4/
│   ├── 0_JOB_SCRIPT.in
│   ├── 1_RELAX_SSZ_13.in
│   ├── 2_RELAX_SSZ_13_1_C2H4.in
│   ├── 3_RELAX_SSZ_13_2_C2H4.in
│   └── 4_RELAX_SSZ_13_3_C2H4.in
├── 05_ELF_SSZ_13_Ag_Al_C2H4/
│   ├── 1_SSZ_13/
│   │   ├── 0_JOB_SCRIPT.in
│   │   ├── 1_SCF.in
│   │   └── 2_PP_ELF.in
│   ├── 2_SSZ_13_1_C2H4/
│   ├── 3_SSZ_13_2_C2H4/
│   └── 4_SSZ_13_3_C2H4/
├── 06_ELF_SSZ_13_C2H4/
│   ├── 1_SSZ_13/
│   ├── 2_SSZ_13_1_C2H4/
│   ├── 3_SSZ_13_2_C2H4/
│   └── 4_SSZ_13_3_C2H4/
├── 07_ENERGY_SSZ_13_Ag_Al_C2H4/
│   ├── 1_SSZ_13/
│   │   ├── 0_JOB_SCRIPT.in
│   │   └── 1_SCF.in
│   ├── 2_SSZ_13_1_C2H4/
│   ├── 3_SSZ_13_2_C2H4/
│   └── 4_SSZ_13_3_C2H4/
├── 08_ENERGY_SSZ_13_C2H4/
│   ├── 1_SSZ_13/
│   ├── 2_SSZ_13_1_C2H4/
│   ├── 3_SSZ_13_2_C2H4/
│   └── 4_SSZ_13_3_C2H4/
├── 09_ENERGY_C2H4/
│   ├── 0_JOB_SCRIPT.in
│   ├── 1_SCF.in
│   └── 2_SCF.in
├── 10_OPTIMIZED_STRUCTURES/
│   └── [xyz/cif files from relaxation outputs]
├── 11_RAW_OUTPUTS/
│   └── [stdout .out files]
└── README.md
```

### D.3 Reproducibility Statement

To reproduce the calculations presented in this thesis:

1. Download the deposited input files from the repository
2. Ensure Quantum ESPRESSO (version 7.2) is installed with appropriate pseudopotentials:
   ```bash
   module load anaconda
   mamba activate qe-7.2
   ```
3. Modify `outdir` and `pseudo_dir` paths in input files to match local environment
4. Submit jobs using provided HPC scripts or run locally:
   ```bash
   pw.x -in [input_file].in > [output_file].out
   ```
5. Extract energies, forces, and properties from output files

**Required Pseudopotentials:** Si.upf, O.upf, Al.upf, Ag.upf, C.upf, H.upf

---

## Appendix E: Glossary of Computational Terms

| Term | Definition |
|------|------------|
| VC-Relax | Volume-constrained relaxation; simultaneous optimization of atomic positions and unit cell parameters |
| SCF | Self-consistent field; iterative solution of Kohn-Sham equations for ground-state energy |
| ELF | Electron localization function; measure of electron pairing probability |
| ecutwfc | Plane-wave kinetic energy cutoff for wavefunctions |
| ecutrho | Plane-wave kinetic energy cutoff for charge density |
| k-point | Sampling point in reciprocal space for Brillouin zone integration |
| BFGS | Broyden-Fletcher-Goldfarb-Shanno; quasi-Newton optimization algorithm |
| USPP | Ultrasoft pseudopotential |
| PAW | Projector augmented-wave |

---

## Notes for Thesis Completion

### Completed Items:

1. **Exchange-Correlation Functional:** PBE-DFT-D3 (vdw_corr='dft-d3')
2. **Quantum ESPRESSO Version:** 7.2
3. **HPC System Details:** 
   - Partition: batch
   - QOS: 240c-1h_batch
   - Nodes: 1, Tasks per node: 40, CPUs per task: 2
   - Memory: 144 GB

### Items to Complete:

1. **Pseudopotential Source:** Specify library (PSlibrary, SSSP, PseudoDojo) and version
   - *Check your QE installation: `$QE_HOME/pseudo/` or where Si.upf, O.upf, etc. are stored*

2. **Repository DOI:** Deposit files and add permanent DOI before final submission
   - Suggested repositories: Materials Cloud, Zenodo, or MSUIIT institutional repository

3. **Email Address:** Update `[EMAIL]` in job script template with your current email

### Figures to Add:

- **Figure A.1:** Visualization of SSZ-13 framework structure
- **Figure A.2:** Ag exchange site in SSZ-13
- **Figure A.3:** C₂H₄ adsorption configurations (1, 2, and 3 molecules)

---

*Last updated: April 9, 2026*
