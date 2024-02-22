---
title: 'How to use AF2'
date: 2024-01-21
tags:
  - AF2
---
### Trying AF2 for predicting protein structure 

If using colabfold on website, remember to disconnect the runtime.

If you are running it locally:
run this bash script from the terminal in the folder containing your PDB files.

Before starting remember to run this command in the folder where you want to run colabfold, in principle the same folder containing the PDB files.
```
export PATH=$PATH:/opt/localcolabfold/localcolabfold/colabfold-conda/bin/
```
You can now save the following script in a bash script "colab_batch.sh", allow to run it (chmod +x colab_batch.sh)  and run it from the terminal.

<img width="646" alt="Screenshot 2024-02-22 at 16 33 46" src="https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/d4a89e4b-6110-4c8e-aa30-a799a613c62f">

```
#!/bin/bash
#colab_batch.sh

#SimoneAttanasio_20240220
#allows you to run colabfold locally in batch on multiple fasta files one after the other.

# Iterate over each .fasta file in the current directory
for fasta_file in *.fasta; do
    # Extract the filename without extension
    filename=$(basename -- "$fasta_file")
    filename_no_ext="${filename%.*}"

    # Create output directory with the same name as the fasta file
    output_dir="${filename_no_ext}_output"
    mkdir -p "$output_dir"

    # Run the command and redirect the output to the output directory
    colabfold_batch "$fasta_file" "$output_dir"
done
```
### How to evaluate colabFold output




---
### References 
- [AF Colab](https://colab.research.google.com/github/deepmind/alphafold/blob/main/notebooks/AlphaFold.ipynb?pli=1) (Source Code)
- [AF Colab2](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb)
- [How to use AF2](https://www.youtube.com/watch?v=eLy7PdzRgLs) (Video)
- [Interpretation of predicted complexes with AF2](https://www.youtube.com/watch?v=_hkxQ8h6L-Q) (Video)
- [ColabFold: making protein folding accessible to all](https://www.nature.com/articles/s41592-022-01488-1) (Nature paper - Mirdita et al. 2022) 
- [Protein complex prediction with AlphaFold-Multimer](https://www.biorxiv.org/content/10.1101/2021.10.04.463034v2.full.pdf) (DeepMind paper - 2022)
- [A structural biology community assessment of AlphaFold2 applications](https://www.nature.com/articles/s41594-022-00849-w) (Akdel et al. 2022)
