---
title: 'Working With PDBs'
date: 2024-05-06
tags:
  - PDB
---

# Working with PDBs 

### Changing residue numbers 

### Separating different chains 
IN case you need to separate a single PDB file into different chains you can do it directly from terminal, using this simple script.

From terminal create a script that you call splitter.sh and authorize the running:
```
nano splitter.sh
chmod +x splitter.sh
```
once the script exist copy paste the following code into splitter.sh

```
#!/bin/bash

# Check if the input file exists
if [ ! -f "$1" ]; then
    echo "Error: Input file does not exist."
    exit 1
fi

# Read input PDB file line by line
while IFS= read -r line; do
    if [[ $line == "ATOM"* ]]; then
        chain_id="${line:21:1}"
        echo "$line" >> "${1%.*}_chain_${chain_id}.pdb"
    fi
done < "$1"
```
to split the PDB, locate in the same folder the executable and the PDB file and run:

```
splitter.sh xxx.pdb
```




... This post is still work in progress 

