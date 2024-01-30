---
title: 'From PDB to Sequence'
date: 2024-01-30
tags:
  - PDB
  - Sequence
  - Python
---
### Python script in the same folder containing your PDBs
<img width="625" alt="Screenshot 2024-01-30 at 18 07 29" src="https://github.com/simoneatt11/simoeatt11.github.io/assets/61795621/4f8b5a31-6760-4eb9-b195-a2cdc022e03b">

!!! The Current script only works if it is located in the same folder where your PDB files are present. If they are in different folders than you need to specify a different directory later on. 

```
pip install biopython
pip install pandas
```


```
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
- Define a Function that can extract the pdb file, the chain id and the corrensponding sequence
- Define the current directory and specify for the pdb files you want to extract the sequence from
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
pdb_files = glob.glob(directory + "*.pdb")

# Data structure to store pdb file names, chain identifiers, and sequences
pdb_sequences = []

# Process each PDB file
for pdb_file in pdb_files:
    sequences = extract_sequence(pdb_file)
    pdb_sequences.extend(sequences)

# Create a pandas DataFrame
df = pd.DataFrame(pdb_sequences, columns=['PDB File', 'Chain ID', 'Protein Sequence'])
```
- Exporting the sequences in a csv file called "pdb_to_sequence"

```
df.to_csv('pdb_to_sequences.csv', index=False)
```
