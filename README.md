Sugar-Binding Residue Predictor (SBRP)
=============
by Masaki Banno at BILAB

Sugar-Binding Residue Predictor (SBRP) is sugar binding prediction tool using support vector machine. SBRP can predict sugar-binding residue from amino acid sequence information. Protein Structure information is not necessary.

#  Installation
SBRP requires python2.7, libsvm, Legacy Blast and nr database.

You can use following links install and download these programs and libraries and database.

- Legacy Blast (blastpgp)
- LIBSVM
- Python2.7x

# Usage
SBRP contains the binding residue predictor for acidic sugar and the binding-residue predictor for nonacidic sugar. Acidic sugar has phosphate group or carboxyl group or sulfate group. NonAcidic Sugar is except for acidic sugar. So, You can get prediction what residue in the protein sequence is belonged to acidic sugar binding residue or nonacidic binding residue.
 
If you download above programs, you can run SBRP like below command.

./SBR_predictor.sh target.fasta

The output example is below.

---
148L:E|PDBID|CHAIN|SEQUENCE 8 -1.67762885786 1.70627963313 False False  
148L:E|PDBID|CHAIN|SEQUENCE 9 -0.49179158867 1.40920844499 False False  
148L:E|PDBID|CHAIN|SEQUENCE 10 1.65258659258 0.973523358096 True False  
148L:E|PDBID|CHAIN|SEQUENCE 11 -1.01298805163 1.14320766578 False False  
148L:E|PDBID|CHAIN|SEQUENCE 12 -0.621458142578 1.37502697583 False False  
148L:E|PDBID|CHAIN|SEQUENCE 13 0.790677700098 0.749706572303 True False  
148L:E|PDBID|CHAIN|SEQUENCE 14 -1.51129664951 1.21914159325 False False  
148L:E|PDBID|CHAIN|SEQUENCE 15 -0.426752423351 0.890993747856 False False  
---

- Column 1 is predicted protein name, this name is equal to header record in FASTA file.
- Column 2 is predicted residue position.
- Column 3 and Column 4 are the decision values of binding residue predictor for acidic sugar and binding residue predictor for non acidic sugar.
- Column 5 and Column 6 are prediction result of acidic sugar binding residue predictor and non sugar binding residue predictor.


# Method
## Dataset
Training dataset is collected from PDB. Sugar binding residue is defined as residues within 4 Å from sugar. The proteins are collected from PDB if the protein has sugar-binding residue.
 
After that, these datasets are refined under the following condition.
The PDB datum which is using the additive for the experiment of sugar.
Residue within 1.5 Å from sugar. (This is not interactions but covalent bond.)
Finally, These proteins are removed redundancy using blastclust.

## Feature Vector
SBRP is using the Position Specific Scoring Matrix (PSSM)  calculated by PSI-Blast for a feature vector of each residue.

## Training method
Support Vector Machine is needed positive dataset and negative dataset. The positive dataset is sugar-binding residue. The negative dataset is within 25 Å without 5 Å from sugar binding residue.
 
