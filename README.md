# Cross-species scRNA-seq analysis of islets cell type, GPCRs expression and GLP1R-GPCR co-expression network
Hormones from pancreatic islets maintain glucose levels, with G protein-coupled receptors (GPCRs) crucial for this balance. GPCR dimerization modulates receptor function, affecting physiological responses. The glucagon-like peptide-1 receptor (GLP1R) is vital for glucose regulation and a target for diabetes treatment.
Utilizing single-cell RNA-sequencing data from mice, rats, pigs, monkeys and human, we performed cross-species analyses to confirm islet cell type conservation, identify conserved GPCR expression and examine their co-expression networks with Glp1r.
<img width="875" alt="image" src="https://github.com/Jihong528/2023_islets_cross_species/assets/50450748/80df4d58-e796-493c-9b40-7b37a303e57d">
<img width="589" alt="image" src="https://github.com/Jihong528/2023_islets_cross_species/assets/50450748/9bf29fdb-818e-4452-b2c8-2abc3a9ca13e">

## Collection of scRNA-seq datasets from vertebrate pancreatic islets
Mouse datasets were derived from the NCBI Gene Expression Omnibus (GEO) with accession numbers GSE84133, GSE128565, and GSE203376. The rat, pig, and monkey datasets were each sourced from GEO with accession numbers GSE203412, GSE198623, and GSE120180, respectively. Human datasets were collected from GEO under accession numbers GSE81547, GSE84133, and GSE114297, as well as from ArrayExpress with accession number E-MTAB-5061.

## Islet scRNA-Seq data processing and cell type annotation
We reanalyzed datasets using Seurat 36 (version 4.0.5) to conduct comprehensive quality control and clustering analyses.
For mice, human, rat, and monkey cells, we set gene count thresholds of 300-6000, 300-4000, 300-3000, and 200-7500, respectively, and excluded cells with mitochondrial/ribosomal mapping rates exceeding 20% for mice and rats, 10% for monkeys and 30% for humans.
The processed pig dataset was retrieved from the online repository at https://cellxgene.cziscience.com/collections/0a77d4c0-d5d0-40f0-aa1a-5e1429bcbd7e. 
Using Canonical Correlation Analysis (CCA), we mitigated intra-dataset batch effects in mouse and human datasets. For rat, pig, and monkey datasets, we applied the Harmony37 package (v0.1.0) to address batch effects. The final curated datasets comprised 15,472 mouse cells, 24,871 human cells, 7,584 rat cells, 2,924 monkey cells, and 20,414 pig cells. The detailed counts for mouse datasets included 1,327 from GSE84133, 7,265 from GSE125865, and 6,880 from GSE203376; for human datasets, 1,626 from GSE81547, 5,383 from GSE84133, 16,109 from GSE114797, and 753 from E-MTAB-5061. 
Cell cluster annotation was refined by utilizing cell type-specific markers: Gcg for alpha cells, Ins1 and Ins2 for beta cells, Sst for delta cells, Ppy for PP cells, and Ghrl or Acsl1 for epsilon cells. 

## GPCR transcriptional expression analysis and Glp1r-GPCR co-expression analysis
G protein-coupled receptors (GPCRs) from mice, rats, pigs, monkeys, and humans were collected from the GPCRdb database43 and Knepper MA paper.44 We utilized one-to-one orthologous GPCRs aligned to the mouse genome for cross-species GPCR analysis.
We assessed GPCR conservation across species by first determining the average expression per GPCR and then assigning quartile-based relative expression levels—'high' (above the third quartile, 3 points), 'medium' (between the first and third quartiles, 2 points), 'low' (below the first quartile, 1 point), and 'absent' (no expression, 0 points). Mice and human GPCR expression scores were doubled to highlight their significance. We then calculated a composite score for each GPCR by summing these weighted points across all species and normalizing them against the maximum potential score to correct for species bias. GPCRs with a normalized score over 0.45 and expressed in a minimum of three cells in at least two different species were classified as conserved.
We selected β-cells expressing Glp1r to explore Glp1r co-expressed with conserved GPCRs. GENIE3 was utilized with Glp1r as the target gene to evaluate the relationship with conserved GPCRs. Using scLink, we constructed Glp1r co-expression network with conserved GPCRs. We further integrated Spearman and Pearson correlations to quantify their interactions. Individual scores from these analyses were standardized and aggregated to form a comprehensive Glp1r-GPCR correlation score for each species. Finally, for a comprehensive assessment across the five species, we calculated an overall score by assigning double weight to mouse and human scores and a single weight to those of the other species. 






