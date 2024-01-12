---
title: 'PyMol tutorial for Alpha Carbon'
date: 2024-01-24
tags:
  - PyMol
---
The “Alpha Carbon” Is The Carbon Adjacent To The Carbonyl group ( C = O )

### Identify Alpha Carbons with PyMol

Using this peptide for tutorial
[peptide.pdb](../files/peptide.pdb)

Open peptide.pdb in pymol

Click on show "S" - show as - wire
![Screenshot 2024-01-12 at 13 22 34](https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/105dd5d1-876e-4f46-a1c5-5ac7ba04eb68)

Click on label "L" - atom name
![Screenshot 2024-01-12 at 13 25 44](https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/1af15be4-00ed-410d-ae4e-98de2417aa63)

Alpha Carbon will be labeled as "CA".

You can create a selection of only CA atoms by running this command in pyMol command window
sele name ca
show spheres, sele

![Screenshot 2024-01-12 at 13 31 03](https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/c99d1ada-7f1d-43ed-816e-6e4758a76864)

You will get an image containing very big spheres at the level of Alpha Carbons, you can render them using the next two commands:
alter sele, vdw=0.5
rebuild

![Screenshot 2024-01-12 at 13 31 44](https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/76cf53ec-7830-4c5f-b3d8-f54c19259b92)

In this way you will have the Alpha Carbons nicely depicted in your structure. 

---
### References
[Protein Structure - Backbone Torsion Angles](http://www.bioinf.org.uk/teaching/bioc0008/page03.html) (teaching article)
[Introduction to Alpha Carbon](https://www.youtube.com/watch?v=3PsZSXB4E3Q) (video)
[What is the Alpha Carbon](https://www.masterorganicchemistry.com/2012/03/26/weird-nomenclature-in-carbonyl-chemistry/#:~:text=The%20%E2%80%9CAlpha%20Carbon%E2%80%9D%20Is%20The%20Carbon%20Adjacent%20To%20The%20Carbonyl,-The%20functional%20group&text=In%20organic%20chemistry%2C%20it's%20common,carbon%E2%80%9D%2C%20and%20so%20on.)
