# Breast Cancer Genomic Analysis: Exploring Molecular Patterns with PCA and LDA

## Motivation

After reading the paper "Genes mirror geography within Europe" about how PCA was used on human genomes in Europe to

## Dataset Overview

This project analyzes the METABRIC (Molecular Taxonomy of Breast Cancer International Consortium) dataset, containing genomic and clinical data from nearly 2,000 primary breast cancer samples. The dataset combines:

- **Clinical data**: Patient demographics, cancer types, treatment approaches, and survival outcomes
- **RNA expression data**: Z-scores for 331 genes representing their expression levels
- **Mutation data**: Binary indicators of mutations across 175 genes
- **Cancer classifications**: Detailed cancer types, histologic subtypes, and molecular clusters

## Exploratory Data Analysis

### Age Distribution and Survival Analysis

![Age Distribution and Survival](Image%201.png)

The age distribution shows most breast cancer diagnoses occur between 60-70 years. The boxplot reveals survival differences across cancer subtypes, with most types showing longer survival for living patients (blue) than deceased patients (purple). Notably, there's considerable variability in survival time within each cancer type, reflecting the heterogeneous nature of breast cancer.

### Cancer Type Distribution and Treatment Approaches

![Cancer Types and Treatment](Image%202.png)

The pie chart shows Breast Invasive Ductal Carcinoma is the predominant type (79.4%), followed by Breast Mixed Ductal and Lobular Carcinoma (11.0%), Breast Invasive Lobular Carcinoma (7.5%), with other types making up the remainder. The treatment bar graph reveals hormone therapy and radiotherapy are more commonly used than chemotherapy, reflecting standard treatment protocols for hormone receptor-positive breast cancers.

### Mutation Count Distribution

![Mutation Distribution](Image%203.png)

The mutation count histogram shows a right-skewed distribution with most patients having 2-8 mutations, but a long tail extends to 80+ mutations in rare cases. This pattern is typical in cancer genomics and may reflect differences in DNA repair mechanisms or tumor evolution paths.

## Principal Component Analysis (PCA)

### What is PCA and Its Application in This Project

Principal Component Analysis is a dimensionality reduction technique that transforms high-dimensional data into a new coordinate system where the axes (principal components) represent directions of maximum variance. In this project, PCA helped:

1. Reduce hundreds of gene measurements to a manageable number of components
2. Visualize relationships between samples in 2D space
3. Identify patterns that might distinguish cancer subtypes
4. Compare RNA expression patterns with mutation patterns

### PCA Results for RNA Expression Data

![RNA PCA Variance](Image%204.png)

The RNA expression variance plot shows that the first few principal components capture a relatively small percentage of the overall variance. Even with 40 components, we only reach about 53% of cumulative explained variance. This indicates high dimensionality in the RNA data, with information distributed across many components.

<!-- ![RNA PCA Plot](Image%205.png) -->
<!-- <iframe src="docs/pca_RNA.html" width="900" height="700" style="border:none;"></iframe> -->

[View Interactive PCA Plot](docs/pca_RNA.html)

The interactive PCA plot of RNA expression data shows the first two principal components, with PC1 explaining 8.00% and PC2 explaining 6.69% of the variance. While there's substantial overlap between cancer types, some patterns emerge:

- Breast Invasive Ductal Carcinoma (blue) is widely distributed, reflecting its heterogeneity
- Breast Invasive Lobular Carcinoma (green) shows some distinct clustering
- The large overlap suggests shared molecular mechanisms across cancer types

The interactive dropdown allows coloring by different clinical variables, enabling exploration of which factors correlate with genetic expression patterns.

### PCA Results for Mutation Data

![Mutation PCA Variance](Image%206.png)

The mutation data variance plot shows a more gradual accumulation of explained variance compared to RNA data. With 40 components, we reach about 64% of cumulative variance, indicating slightly better dimensionality reduction potential than RNA data.

![Mutation PCA Plot](Image%207.png)

The mutation PCA plot reveals a distinctive pattern with several distinct clusters, suggesting that mutation profiles might better separate cancer subtypes than expression profiles. PC1 explains 6.44% and PC2 explains 4.69% of variance. The plot shows:

- Multiple well-defined clusters that don't directly correlate with conventional cancer types
- These clusters likely represent different mutational signatures or processes
- The separation is clearer than in the RNA PCA, suggesting mutation data might be more informative for subtyping

### Comparing RNA and Mutation PCA Results

The RNA and mutation PCA analyses provide complementary views of breast cancer biology:

1. **Explained variance**: Both analyses require many components to explain substantial variance, reflecting the complexity of cancer biology, but mutation data appears slightly more reducible.

2. **Clustering patterns**: Mutation data shows more distinct clustering than RNA expression, suggesting that genetic alterations might provide clearer molecular subtypes.

3. **Biology interpretation**:

   - RNA patterns reflect the functional state of cancer cells (what genes are active)
   - Mutation patterns reveal the underlying genetic alterations driving the disease

4. **Clinical relevance**: The interactive visualizations allow exploration of how molecular patterns relate to clinical variables, potentially revealing biomarkers or treatment targets.

## Linear Discriminant Analysis (LDA)

### What is LDA and How It Complements PCA

Linear Discriminant Analysis is a supervised dimensionality reduction technique that finds linear combinations of features that best separate predefined classes. Unlike PCA (which maximizes variance regardless of class), LDA specifically optimizes for class separation. In this project, LDA:

1. Provides a complementary view to PCA by focusing on features that distinguish cancer types
2. Helps identify genetic signatures associated with specific clinical variables
3. Offers a supervised approach to understanding molecular subtypes

### LDA Results for RNA Expression Data

![RNA LDA by Cancer Type](Image%208.png)

The LDA plot for RNA expression data by cancer type shows remarkably good separation between cancer subtypes, especially for Breast Invasive Lobular Carcinoma (green) which forms a distinct cluster. This indicates that gene expression contains strong signals that can differentiate these histological types, despite the overlap seen in PCA.

![RNA LDA by Histologic Subtype](Image%209.png)

When targeting histologic subtypes, the RNA LDA reveals excellent separation of Lobular carcinomas (green) and Medullary carcinomas (light blue). The clear clustering demonstrates that gene expression profiles strongly correlate with histological features observed under microscope examination.

![RNA LDA by Integrative Cluster](Image%2010.png)

The integrative cluster LDA shows remarkable separation between molecular subtypes, particularly cluster 10 (light green) and cluster 5 (light blue). The clear boundaries between these clusters validate the molecular taxonomy approach to breast cancer classification and suggest distinct biological mechanisms underlying each subtype.

![RNA LDA by Histologic Grade](Image%2011.png)

The LDA by histologic grade shows less distinct separation, with considerable overlap between grades. This suggests that while gene expression can partially predict tumor grade, other factors also influence this pathological assessment.

### LDA Results for Mutation Data

![Mutation LDA by Cancer Type](Image%2012.png)

The mutation data LDA for cancer types shows clear separation of Breast Invasive Lobular Carcinoma (green), similar to the RNA results. This indicates that both gene expression and mutation profiles can distinguish lobular carcinomas from other types, suggesting fundamental biological differences.

![Mutation LDA by Histologic Subtype](Image%2013.png)

The mutation LDA by histologic subtype shows patterns similar to the RNA analysis, but with some differences in cluster shapes and separations. Lobular carcinomas (green) remain well-separated, indicating consistent molecular signatures across both expression and mutation analyses.

![Mutation LDA by Integrative Cluster](Image%2014.png)

The integrative cluster LDA for mutation data shows less distinct clustering than the RNA analysis, suggesting that the molecular subtypes are defined more by expression patterns than by specific mutations.

![Mutation LDA by Histologic Grade](Image%2015.png)

The mutation LDA by grade shows some separation between grade 3 tumors (blue) and others, indicating that higher-grade tumors may have distinctive mutation patterns. Unlike RNA data, there appears to be better separation by grade using mutation data.

### Comparing RNA and Mutation LDA Results

The LDA analyses reveal important insights about breast cancer molecular classification:

1. **Classification power**: Both RNA and mutation data can separate cancer subtypes, but RNA appears generally more effective, especially for molecular subtypes.

2. **Cancer type distinction**: Lobular carcinoma consistently separates from other types in both analyses, confirming its distinct biological nature.

3. **Histologic correlation**: Gene expression shows stronger correlation with histologic features than mutation data.

4. **Integrative clusters**: These molecular subtypes are better defined by expression patterns than mutation profiles, as shown by the clearer clustering in RNA LDA.

5. **Tumor grade**: Mutation profiles show better separation by grade than expression data, suggesting that certain mutations may drive aggressive behavior.

## Interactive Visualization Tools

A key feature of this project is the interactive visualization capability:

1. **PCA visualizations**: Allow coloring by multiple clinical variables through a convenient dropdown menu
2. **LDA visualizations**: Provide dual-dropdown functionality to select both the target and color variables
3. **Hover functionality**: Shows detailed information for each data point

These tools transform static analyses into dynamic, exploratory interfaces that facilitate discovery of relationships between genetic profiles and clinical features.

## Conclusion

This analysis of the METABRIC breast cancer dataset demonstrates the complementary power of unsupervised (PCA) and supervised (LDA) dimensionality reduction techniques in revealing molecular patterns in cancer genomics.

Key findings include:

1. RNA expression and mutation data provide different but complementary views of breast cancer biology, with mutations showing more distinct clustering in PCA and RNA showing better separation in LDA.

2. Breast Invasive Lobular Carcinoma emerges as molecularly distinct from other subtypes in both analyses, suggesting fundamental biological differences.

3. Integrative molecular clusters show remarkable separation in RNA LDA, validating their biological relevance as distinct disease entities.

4. Interactive visualizations enable exploration of relationships between molecular patterns and clinical variables, potentially revealing biomarkers and treatment targets.

This project highlights how computational approaches can uncover patterns in complex cancer genomics data that may not be apparent through conventional analyses. The findings could contribute to improved molecular classification, biomarker development, and ultimately personalized treatment approaches for breast cancer patients.

## Sources

1. Pereira, B., Chin, S.F., Rueda, O.M. et al. (2016). The somatic mutation profiles of 2,433 breast cancers refine their genomic and transcriptomic landscapes. Nature Communications, 7, 11479.

2. Curtis, C., Shah, S.P., Chin, S.F. et al. (2012). The genomic and transcriptomic architecture of 2,000 breast tumours reveals novel subgroups. Nature, 486, 346-352.

3. Jolliffe, I.T. & Cadima, J. (2016). Principal component analysis: a review and recent developments. Philosophical Transactions of the Royal Society A, 374, 20150202.

4. Fisher, R.A. (1936). The use of multiple measurements in taxonomic problems. Annals of Eugenics, 7, 179-188.

5. Tharwat, A., Gaber, T., Ibrahim, A., & Hassanien, A.E. (2017). Linear discriminant analysis: A detailed tutorial. AI Communications, 30, 169-190.

6. Ringner, M. (2008). What is principal component analysis? Nature Biotechnology, 26, 303-304.
