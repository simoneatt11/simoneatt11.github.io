---
title: 'From PDB to Sequence'
date: 2024-01-30
tags:
  - PDB
  - Sequence
  - Python
---

### Installing Biopython
```
pip install biopython
pip install pandas

import glob
from Bio.PDB import PDBParser
import pandas as pd

# Dictionary for converting three-letter amino acid codes to one-letter codes
aa_three_to_one = {
    "ALA": "A", "ARG": "R", "ASN": "N", "ASP": "D", "CYS": "C",
    "GLN": "Q", "GLU": "E", "GLY": "G", "HIS": "H", "ILE": "I",
    "LEU": "L", "LYS": "K", "MET": "M", "PHE": "F", "PRO": "P",
    "SER": "S", "THR": "T", "TRP": "W", "TYR": "Y", "VAL": "V"
}
```


```
def extract_sequence(pdb_file):
    parser = PDBParser()
    structure = parser.get_structure("structure", pdb_file)
    sequences = []
    for model in structure:
        for chain in model:
            sequence = ""
            for residue in chain:
                res_name = residue.get_resname()
                if res_name in aa_three_to_one:  # standard amino acids
                    sequence += aa_three_to_one[res_name]
            if sequence:  # Add only if sequence is not empty
                sequences.append((pdb_file, chain.id, sequence))
    return sequences

# Use "./" to specify the current directory
directory = "./"

# Find all PDB files in the current directory using a wildcard
pdb_files = glob.glob(directory + "*.pd*")

# Data structure to store pdb file names, chain identifiers, and sequences
pdb_sequences = []

# Process each PDB file
for pdb_file in pdb_files:
    sequences = extract_sequence(pdb_file)
    pdb_sequences.extend(sequences)

# Create a pandas DataFrame
df = pd.DataFrame(pdb_sequences, columns=['PDB File', 'Chain ID', 'Protein Sequence'])
```

