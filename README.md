# scRNA-Seq-Analysis

The goal of this analysis is to perform a scRNA-seq pipeline between two different conditions: Healthy lung cells and Eml4-Alk mutant cells with NSCLC (Non-small-cell lung cancer) in mice. The Eml4-Alk mutation results as a fusion between a portion of the EML4 gene with the ALK gene, which leads to an abnormal protein that drives cancer growth, in this specific case lung cancer.

Single cell suspensions were prepared from excised lungs of Eml4-Alk and wild type C57/Bl6J mice [1]. Suspensions were pooled from n=3 mice per condition, and then were enriched for cell viability and depleted for CD45+ cells to remove inmune cells from the mixture[1]. The experimental flow can be seen in the figure above.

Single cells were processed using the 10X Genomics Single Cell 3’ platform using the Chromium Single Cell 3’ Library & Gel Bead Kit V2 kit (10X Genomics). The libraries were sequenced using an Illumina NovaSeq6000 sequencer on an Illumina NovaSeq SP flow cell [1].

## Data set description
The data used here can be accessed here: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE191078

It consists of two count matrices:

Wild Type lung cells
Eml4-Alk lung cells
### 1. Read the Count matrices
The coun matrices were downloaded from the link above into the corresponding jupyter folder. Using scanpy package in python both data sets were save as AnnData objects.

Wild Type: adata1, it contains 15867 cells and 32285 genes.
Eml4-Alk: adata2, it contains 21856 cells and 32285 genes.

### 2. Quality Control
#### 2.1 Doublets
To filter doublet cells in the count matrices, Scrublet was used. With a expected doublet rate of 0.07. The predicted score of doublet is going to be save in the data objects so it can be filter further ahead in the analysis.
### 2.2 QC Filtering
Some initial filtering based on count has to be performed for both datasets. This is done to remove barcodes that correspondto broken or no cells. The threshold here is 200 genes with a minimum of 3 cells.

Wild Type: adata1, after filtering contains 14817 cells and 17425 genes.
Eml4-Alk: adata2, after filtering 20055 cells and 18891 genes.

### 3. Combining both datasets into one data object
Both data sets were combined into one using the concatenate function in python. A sample id column was added to differentiate between WT and EA.

## Conclusions
From the integrated scRNA-seq analysis comparing healthy lung cells to Eml4-Alk mutant lung cells, several key findings emerge from the clustering and differential gene expression analyses, particularly related to cell annotations and enriched biological processes:

### Cellular Composition and Annotations: The clustering analysis identified seven distinct cell clusters, each representing specific cell types or subtypes within the lung tissue:

Capillary Endothelium (General) and Capillary Endothelium (Aerocyte):
Identified two subsets of capillary endothelial cells, suggesting potential heterogeneity within endothelial populations, possibly associated with functional specialization or response to the Eml4-Alk mutation [1].

Alveolar Epithelium (AT1 + AT2):
Recognition of alveolar epithelial cells, including AT1 and AT2 subtypes, crucial for gas exchange, and ciliated epithelium involved in airway maintenance, indicating representation of key lung cell types [1].

Stroma (Fibroblasts, SMCs, Pericytes):
Presence of stromal cell types (fibroblasts, smooth muscle cells, pericytes), suggesting their involvement in lung tissue structure, regulation, and potential alterations in the mutant condition [1].

Lymphatic Endothelium:
Distinct identification of endothelial subtypes (lymphatic) and club cells, hinting at differences in vascular specialization and specific epithelial cell functions between healthy and mutant conditions [1].

### Enriched Biological Processes:

The analysis of differentially expressed genes (DEGs) and gene ontology (GO) terms enrichment highlighted significant associations with processes related to vasculature development, tube morphogenesis, and blood vessel development.

The enrichment of these GO terms indicates that genes differentially expressed between healthy and Eml4-Alk mutant lung cells are significantly involved in regulating the formation, shaping, and development of blood vessels and related structures.

The scRNA-seq analysis revealed alterations in cellular composition, suggesting potential changes in endothelial subtypes, epithelial cells, and stromal components between healthy and Eml4-Alk mutant lung tissues. The enrichment of GO terms related to vascular development signifies a potential impact of the Eml4-Alk mutation on processes crucial for blood vessel formation and tube morphogenesis within the lung.

This comprehensive characterization points towards potential shifts in cellular populations and biological processes associated with lung tissue function and development affected by the Eml4-Alk mutation. Further investigation into the identified cell types, specific gene expression profiles, and functional validations would deepen our understanding of the molecular mechanisms underlying the mutation's effects on lung biology and disease progression.

## References
[1] Amini, A.P., Kirkpatrick, J.D., Wang, C.S. et al. Multiscale profiling of protease activity in cancer. Nat Commun 13, 5745 (2022). https://doi.org/10.1038/s41467-022-32988-5
