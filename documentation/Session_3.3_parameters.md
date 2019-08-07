# mOTUs Parameters

There are number of optional parameters that can be provided to ***profile*** to modify the output format, but not the actual mOTUs algorithm.

```bash
   -I FILE         save the result of bwa in bam format (intermediate step) [None]
   -M FILE         save the mgc reads count (intermediate step) [None]
   -e              profile only reference species (ref_mOTUs)
   -c              print result as counts instead of relative abundances
   -p              print NCBI id
   -u              print the full name of the species
   -q              print the full rank taxonomy
   -B              print result in BIOM format
   -C STR          print result in CAMI format (BioBoxes format 0.9.1)
                   Values: [precision, recall, parenthesis]
   -k STR          taxonomic level [mOTU]
                   Values: [kingdom, phylum, class, order, family, genus, mOTU]
```

We can for instance modify our output to see counts, rather than relative abundances, and move our analysis to the family level, but only allowing reference species:

```bash
motus profile 
