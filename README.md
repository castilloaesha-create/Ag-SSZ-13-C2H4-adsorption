# DFT Calculations: Ethylene Adsorption on Ag-SSZ-13 Zeolite

## Description
This repository contains Density Functional Theory (DFT) input files and computational data for studying ethylene (C₂H₄) adsorption on silver-exchanged SSZ-13 zeolite frameworks.

## Computational Details

- **Software:** Quantum ESPRESSO v7.2
- **Functional:** PBE-DFT-D3 (Grimme's D3 dispersion corrections)
- **Plane-wave cutoff:** 60 Ry
- **Charge density cutoff:** 240 Ry
- **SCF convergence:** 1.0 × 10⁻⁸ Ry
- **Force convergence:** 1.0 × 10⁻³ Ry/bohr

## Repository Structure

```
Output/
├── 1_VC_RELAX/                    # Initial volume-constrained relaxation
├── 2_VC_RELAX_no_Al_Ag/          # Unsubstituted SSZ-13 relaxation
├── 3_VC_RELAX_SSZ_13_Al_Ag_C2H4/ # Ag-SSZ-13 + C₂H₄ relaxations (1,2,3 molecules)
├── 4_VC_RELAX_SSZ_13_C2H4/       # SSZ-13 + C₂H₄ relaxations
├── 5_ELF_SSZ_13_Ag_Al_C2H4/      # ELF analysis (Ag-exchanged systems)
├── 6_ELF_SSZ_13_C2H4/            # ELF analysis (unsubstituted systems)
├── 7_ENERGY_SSZ_13_Ag_Al_C2H4/   # SCF energy calculations (Ag-exchanged)
├── 8_ENERGY_SSZ_13_C2H4/         # SCF energy calculations (unsubstituted)
├── 9_ENERGY_C2H4/                # Isolated ethylene energy calculations
└── APPENDICES_DRAFT.md           # Manuscript appendices draft
```

## Systems Studied

| System | Description | Atoms |
|--------|-------------|-------|
| S1 | Ag-SSZ-13 (pristine) | 109 |
| S2 | SSZ-13 (Si-only) | 108 |
| S3 | Ag-SSZ-13 + 1 C₂H₄ | 115 |
| S4 | Ag-SSZ-13 + 2 C₂H₄ | 121 |
| S5 | Ag-SSZ-13 + 3 C₂H₄ | 127 |
| S6 | C₂H₄ (gas phase) | 6 |

## Adsorption Energy Calculation

```
E_ads = E(Ag-SSZ-13 + nC2H4) - E(Ag-SSZ-13) - n × E(C2H4)
```

where n = 1, 2, or 3 ethylene molecules.

## How to Run Calculations

1. Load Quantum ESPRESSO environment:
   ```bash
   module load anaconda
   mamba activate qe-7.2
   ```

2. Run a calculation:
   ```bash
   pw.x -in [input_file].in > [output_file].out
   ```

3. Or use the provided SLURM scripts:
   ```bash
   sbatch 0_JOB_SCRIPT.in
   ```

## Pseudopotentials

Required UPF files:
- Si.upf
- O.upf
- Al.upf
- Ag.upf
- C.upf
- H.upf

*Note: Pseudopotential source to be specified.*

## Author

**Art Anthony Munio**  
Mindanao State University - Iligan Institute of Technology  
Email: arthanthony.munio@g.msuiit.edu.ph

## License

This computational data is provided for research and educational purposes.

## Citation

If you use this data in your research, please cite:

```
[Thesis citation to be added upon publication]
```

---

*Last updated: April 9, 2026*
