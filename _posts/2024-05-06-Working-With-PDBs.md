---
title: 'Working With PDBs'
date: 2024-05-06
tags:
  - PDB
---
last modification 20240910 - Adding Rscript for changing residues. 
PDB_residueChanger.R

# Working with PDBs 

### Changing residue numbers 

Just found a page where everything is already present - [pdb-tools](https://www.bonvinlab.org/pdb-tools/)

### Renumbering a PDB 
When renumbering check that the new 3D structure is not altered.

```
# Install and load required packages
install.packages("bio3d")
library(bio3d)

pdb <- read.pdb("~/path/to/your/file.pdb")

# Extract atomic coordinates
coords <- pdb$atom

# change the number (32) and adjust "+" or "-" depending on what is needed
coords$resno <- coords$resno + 32

# Create a new pdb
pdb_new <- pdb
pdb_new$atom <- coords

# Write modified PDB file
write.pdb(pdb_new, file = "file.pdb")

```

### Separating different chains 
If you need to separate a single PDB file into different chains you can do it directly from terminal, using this simple script.

From terminal create a script that you call splitter.sh and authorize the running:
```
nano splitter.sh
chmod +x splitter.sh
```
once you create the script, copy paste the following code into splitter.sh

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
./splitter.sh xxx.pdb
```
In case your PDB file does not start immediately but has some lines before, like in the following example, you can specify at which line the chain separation should start. 
![Screenshot 2024-05-06 at 15 28 45](https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/ee2d515b-7150-4560-adc0-df27eaca2b34)

As before you can create a script that you can easily modify depending on your needs:

```
#!/bin/bash

# Check if the input file exists
if [ ! -f "$1" ]; then
    echo "Error: Input file does not exist."
    exit 1
fi

# Start reading from line 246
line_number=0
while IFS= read -r line; do
    ((line_number++))
    if [[ $line_number -ge 246 && $line == "ATOM"* ]]; then #change 246 with the number at which your PDB file starts
        chain_id="${line:21:1}"
        echo "$line" >> "${1%.*}_chain_${chain_id}.pdb"
    fi
done < "$1"
```

Running this script called splitterStart.sh and modifying the 246 with the number you need, you can easily divide your PDB in different chains. 



... This post is still work in progress 

