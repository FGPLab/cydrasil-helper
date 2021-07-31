# Pipeline for Generating Phylogeny

## Alignment with SSU-Align

`ssu-prep -x cydrasil-v3-sequence-list.fasta cydrasil-3-ssu-align 6`

`bash cydrasil-3-ssu-align.ssu-align.sh`

`ssu-mask cydrasil-3-ssu-align`

```
from Bio import AlignIO

input_handle = open("alignment-work\cydrasil-3-ssu-align\cydrasil-3-ssu-align.bacteria.mask.stk", "rU")
output_handle_fa = open("Cydrasil-v3-aln-mask.afa", "w")
output_handle_rel-phy = open("Cydrasil-v3-aln-mask.phy", "w")

alignments = AlignIO.parse(input_handle, "stockholm")
AlignIO.write(alignments, output_handle_fa, "fasta")
AlignIO.write(alignments, output_handle_rel-phy, "phylip-relaxed")

output_handle_fa.close()
output_handle_rel-phy.close()
input_handle.close()

```
## Model tests were ran on [CIPRES](https://www.phylo.org/)

I have included the commands executed by CIPRES, along with the best scoring models. 

### modeltest-ng

`modeltest-ng -p 22 -v -i infile.phy -t ml -o output+G -h g -s 11`

modeltest-ng/+G:    SYM+G4            BIC: 252659.3496

`modeltest-ng -p 22 -v -i infile.phy -t ml -o output+G+I -h f -s 11`

modeltest-ng/+I+G:  TVM+I+G4          BIC: 266330.3807

### iqtree

`iqtree2 -nt 6 -st DNA -s infile.txt -seed 42 --prefix output`

iq-tree: TVMe+R9                      BIC: 264862.6217

## Phylogeny was genrated using RAxML-ng on [CIPRES](https://www.phylo.org/)

`raxml-ng --threads 80 --force perf_threads -msa infile.txt --workers 20 --bs-trees autoMRE{1000} --seed 42 --all --model SYM+G4 --prefix cy-v3-sym+g4`
