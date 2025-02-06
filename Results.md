Title:  "Genome assembly for 10 Salmonella Reading strains"
Author: "Sathesh K. Sivasankaran"
Date:   "Nov 27, 2019"
---
# Genome assembly of 10 Salmonella Reading strains

## Results.

### Reading Strains harbor extra-chromosomal DNA.
All strains harbor one 4.68MB chromosome with one or more small contigs. Length of the small contigs vary from ~10 - 1.5 KB. Four post outbreak strains (SX444, 45, 47 & 48) contain a small 134bp sequence with very high read coverage. The plasmid type of each strain were analyzed using Abricate, results were documented in "Reading_Assembly_Results_10232019.xlsx" (sheet-Abricate_Result).

| Strain | Chro | Length  | Coverage | Circular |
|--------|------|---------|----------|----------|
| SX439  | 1    | 4682296 | 1.00x    | TRUE     |
| SX439  | 2    | 2096    | 65.93x   | TRUE     |
| SX439  | 3    | 1526    | 78.79x   | TRUE     |
| SX440  | 1    | 4681815 | 1.00x    | TRUE     |
| SX440  | 2    | 10911   | 19.50x   | TRUE     |
| SX440  | 3    | 2118    | 154.13x  | TRUE     |
| SX440  | 4    | 2096    | 148.61x  | TRUE     |
| SX441  | 1    | 4682645 | 1.00x    | TRUE     |
| SX441  | 2    | 2096    | 50.07x   | TRUE     |
| SX441  | 3    | 1527    | 60.51x   | TRUE     |
| SX442  | 1    | 4682281 | 1.00x    | TRUE     |
| SX442  | 2    | 2096    | 51.22x   | TRUE     |
| SX442  | 3    | 1527    | 57.13x   | TRUE     |
| SX443  | 1    | 4681306 | 1.00x    | TRUE     |
| SX443  | 2    | 7319    | 13.88x   | TRUE     |
| SX443  | 3    | 2096    | 41.51x   | TRUE     |
| SX444  | 1    | 4647276 | 1.00x    | TRUE     |
| SX444  | 2    | 10384   | 7.86x    | TRUE     |
| SX444  | 3    | 2123    | 39.23x   |          |
| SX444  | 4    | 1962    | 42.92x   |          |
| SX444  | 5    | 134     | 80.76x   |          |
| SX445  | 1    | 4647125 | 1.00x    | TRUE     |
| SX445  | 2    | 2123    | 31.35x   |          |
| SX445  | 3    | 1962    | 33.45x   |          |
| SX445  | 4    | 134     | 63.59x   |          |
| SX446  | 1    | 4647502 | 1.00x    | TRUE     |
| SX446  | 2    | 10911   | 12.59x   | TRUE     |
| SX446  | 3    | 10384   | 8.75x    | TRUE     |
| SX446  | 4    | 4353    | 65.55x   | TRUE     |
| SX447  | 1    | 4647485 | 1.00x    | TRUE     |
| SX447  | 2    | 10384   | 7.16x    | TRUE     |
| SX447  | 3    | 2123    | 41.49x   |          |
| SX447  | 4    | 1962    | 47.50x   |          |
| SX447  | 5    | 1527    | 53.48x   | TRUE     |
| SX447  | 6    | 134     | 101.67x  |          |
| SX448  | 1    | 4647277 | 1.00x    | TRUE     |
| SX448  | 2    | 2123    | 48.04x   |          |
| SX448  | 3    | 1962    | 42.45x   |          |
| SX448  | 4    | 1527    | 51.87x   | TRUE     |
| SX448  | 5    | 134     | 88.56x   |          |

Reading genomes were annotated using Prokka, result GFF files were located on //.

### A stretch of Phage-like genes were missing in post-outbreak strains.
Pan-genome analysis to identify genome difference between pre- and post-outbreak using Roary. Our analysis revealed a stretch of phage-like genes (31 genes) were missing from the post-outbreak strains. A couple of genes (hypothetical proteins) were inserted specifically to post-outbreak strains.

CirA which encodes colicin I receptor was truncated in the pre-outbreak Reading strains. The results were documented in "Reading_Assembly_Results_10232019.xlsx" (sheets: Present and absent & Length_Differences).

### SNP analysis.
Our analysis found 12 SNPs were different between pre- and post-outbreak strains. Deep analysis and interpretation are required to further establish SNP based results. The SNP results were documented in "Reading_Assembly_Results_10232019.xlsx" (sheets: SNP Chro1 & SNP Chro3).


### ABricate results.

| Strain | Chromosome | START | END  | GENE    | COVERAGE   | COVERAGE_MAP     | GAPS |  %COVERAGE | %IDENTITY | DATABASE      | ACCESSION | PRODUCT             |
| ------ | ---------- | ----- | ---- | ------- | ---------- | ---------------- | ---- | ---------- | --------- | ------------- | --------- | ------------------- |
| SX439  | 2          | 1877  | 2069 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 98.96     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX440  | 2          | 198   | 647  | IncQ1   | 1-450/450  | \=============== | 0/0  | 100        | 100       | plasmidfinder | HE654726  | IncQ1_1__HE654726   |
| SX440  | 4          | 1877  | 2069 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 98.96     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX441  | 2          | 1487  | 1679 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 98.96     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX442  | 2          | 1877  | 2069 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 98.96     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX443  | 2          | 4146  | 4265 | ColRNAI | 13-130/130 | .=======/======  | 2/2  | 90.77      | 89.17     | plasmidfinder | DQ298019  | ColRNAI_1__DQ298019 |
| SX443  | 3          | 1878  | 2070 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 98.96     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX444  | 2          | 7055  | 7183 | ColRNAI | 1-128/130  | \========/====== | 1/1  | 98.46      | 84.5      | plasmidfinder | DQ298019  | ColRNAI_1__DQ298019 |
| SX444  | 3          | 2     | 87   | ColpVC  | 1-86/193   | \=======........ | 0/0  | 44.56      | 94.19     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX444  | 4          | 1     | 87   | ColpVC  | 1-87/193   | \=======........ | 0/0  | 45.08      | 97.7      | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX444  | 5          | 1     | 106  | ColpVC  | 88-193/193 | ......=========  | 0/0  | 54.92      | 100       | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX445  | 2          | 2037  | 2122 | ColpVC  | 1-86/193   | \=======........ | 0/0  | 44.56      | 94.19     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX445  | 3          | 1876  | 1962 | ColpVC  | 1-87/193   | \=======........ | 0/0  | 45.08      | 97.7      | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX445  | 4          | 29    | 134  | ColpVC  | 88-193/193 | ......=========  | 0/0  | 54.92      | 100       | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX446  | 2          | 198   | 647  | IncQ1   | 1-450/450  | \=============== | 0/0  | 100        | 100       | plasmidfinder | HE654726  | IncQ1_1__HE654726   |
| SX446  | 3          | 9262  | 9390 | ColRNAI | 1-128/130  | \========/====== | 1/1  | 98.46      | 84.5      | plasmidfinder | DQ298019  | ColRNAI_1__DQ298019 |
| SX446  | 4          | 1463  | 1655 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 96.89     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX446  | 4          | 3720  | 3912 | ColpVC  | 1-193/193  | \=============== | 0/0  | 100        | 98.96     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX447  | 2          | 9455  | 9583 | ColRNAI | 1-128/130  | \========/====== | 1/1  | 98.46      | 84.5      | plasmidfinder | DQ298019  | ColRNAI_1__DQ298019 |
| SX447  | 3          | 2037  | 2122 | ColpVC  | 1-86/193   | \=======........ | 0/0  | 44.56      | 94.19     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX447  | 4          | 1     | 87   | ColpVC  | 1-87/193   | \=======........ | 0/0  | 45.08      | 97.7      | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX447  | 6          | 29    | 134  | ColpVC  | 88-193/193 | ......=========  | 0/0  | 54.92      | 100       | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX448  | 2          | 2     | 87   | ColpVC  | 1-86/193   | \=======........ | 0/0  | 44.56      | 94.19     | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX448  | 3          | 1876  | 1962 | ColpVC  | 1-87/193   | \=======........ | 0/0  | 45.08      | 97.7      | plasmidfinder | JX133088  | ColpVC_1__JX133088  |
| SX448  | 5          | 29    | 134  | ColpVC  | 88-193/193 | ......=========  | 0/0  | 54.92      | 100       | plasmidfinder | JX133088  | ColpVC_1__JX133088  |

