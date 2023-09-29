## GBS-SBG 
Group B Streptococcus serotyping by genome sequencing. 
[github link](https://github.com/swainechen/GBS-SBG)   

Assembly based serotype calling  
```
usage: 
GBS-SBG.pl <assembly_fasta_file> [ -name <string> ] [ -best ] [ -blastn <path_to_blastn> ] [ -ref <GBS-SBG references> ] [ -debug ]
```

basic command:  
```
GBS-SBG.pl assemblyfile.fasta -name assemblyname
```


Tools included:  
*  blast (2.14.1+)
*  gbs-sbg (20230926)  



## Reference 
*   Tiruvayipati, et al. "GBS-SBG - GBS Serotyping by Genome Sequencing." Microb Genom. 2021 Dec;7(12). doi: 10.1099/mgen.0.000688  


