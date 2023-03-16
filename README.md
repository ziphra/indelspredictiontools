## Indels prediction tools

The classification of the pathogenicity of candidate causal variants is essential for robust diagnosis and management of genetic disorders. In silico pathogenicity prediction algorithms are widely used to predict the impact of variation on protein function. These algorithms incorporate various lines of evidence to produce a score used to assign pathogenicity status to a given variant. Most pathogenicity predictors have been developed to predict the effect of missense substitutions, but small insertions and deletions (indels) account for a significant proportion of variation in the human genome and have been linked to numerous rare heritable diseases.

The following article evaluated the performance of nine different tools used to predict the pathogenicity of in-frame indels (insertions and deletions).

> Cannon, S., Williams, M., Gunning, A.C. et al. Evaluation of in silico pathogenicity prediction tools for the classification of small in-frame indels. BMC Med Genomics 16, 36 (2023). https://doi.org/10.1186/s12920-023-01454-6

The tools were tested on a dataset of 3,964 in-frame indels and a smaller subset of 151 novel, clinically classified indels that are not readily accessible from public databases. The study found that the tools performed well across a range of indel lengths, with AUCs (area under the curve) ranging from 0.81 to 0.93. However, most tools performed less well on the smaller, novel subset, with AUCs ranging from 0.64 to 0.87, likely reflecting the use of publicly accessible datasets in the tools' classification method or training data. MutationTaster2021 had the highest sensitivity and specificity when tested on all variants, but also showed the greatest decrease in sensitivity when tested on the DDD only dataset. The study found that the pathogenicity predictor tools varied substantially in input requirements and ease of use. The study noted limitations in the dataset used, including uncertainties in the veracity of variant classifications taken from ClinVar, DDD, and gnomAD databases, the relative rarity of in-frame indels, and the difficulty of detecting large in-frame indels using short-read NGS technologies.

Out of the 9 tools benchmarked in this article, only the ones having a CLI and supporting genome build 38 will be further tested.

Useful metrics: 

- **Sensitivity:** proportion of true positive results
- **Sensibility:** proportion of true negative results
- **LR+**: it indicates how much more likely a true positive result is compared to a false positive result, and is calculated as *sensitivity / (1 - specificity)*. A high LR+ value means that a positive result is a strong indicator of the condition being present.
- **LR-:** it indicates how much more likely a false negative result is compared to a true negative result, and is calculated as *(1 - sensitivity) / specificity*. A low LR- value means that a negative result is a strong indicator of the condition being absent.
- **PPV:** Positive Predictive Value. *PPV = TP / (TP + FP)*. It is the probability that a positive result truly indicates the presence of the condition of interest. However, PPV is affected by the prevalence of the condition in the population being tested, so it is important to consider this when interpreting PPV values.
- **NPV:** Negative Predictive Value. *NPV = TN / (TN + FN)*.  The NPV is the proportion of people who test negative and are truly negative, out of all the people who test negative. The higher, the better.
- **AUC:** It is a common metric used to evaluate the performance of a binary classifier, such as those in machine learning and diagnostic testing. It represents the ability of the classifier to distinguish between positive and negative cases. The AUC is calculated by plotting the true positive rate (TPR) against the false positive rate (FPR) at different classification thresholds and calculating the area under the resulting curve. Higher AUC values indicate better classifier performance in terms of distinguishing between positive and negative cases.
- **MCC:** The Matthews correlation coefficient (MCC) is a measure of the quality of binary (two-class) classifications. It takes into account true and false positives and negatives and is generally regarded as a balanced measure that can be used even if the classes are of very different sizes.
The MCC ranges between -1 and +1, where +1 indicates a perfect prediction, 0 indicates a random prediction, and -1 indicates a total disagreement between prediction and observation. MCC can be calculated using the following formula:
*MCC = (TP x TN - FP x FN) / sqrt((TP + FP) x (TP + FN) x (TN + FP) x (TN + FN))*




## Performance metrics for all indel pathogenicity prediction tools tested
### All variants (1740 pathogenic; 2224 benign)

| **Tool**               | **TP** | **FP** | **TN** | **FN** | **Total(%)** | **Sns** | **Spec** | **LR+** | **LR-** | **PPV** | **NPV** | **AUC** | **MCC** |
|------------------------|--------|--------|--------|--------|--------------|---------|----------|---------|---------|---------|---------|---------|---------|
| **CADD**               | 852    | 176    | 2047   | 886    | 3961(99.9)   | 0.49    | 0.92     | 6.19$   | 0.55    | 0.83    | 0.7     | 0.86    | 0.47    |
| **CAPICE**             | 1611   | 715    | 1500   | 129    | 3955(99.7)   | 0.93    | 0.68     | 2.87+   | 0.11+   | 0.69    | 0.92    | 0.91    | 0.61    |
| **FATHMM-Indel**       | 1626   | 572    | 1622   | 111    | 3931(99.2)   | 0.94    | 0.74     | 3.59+   | 0.09+   | 0.74    | 0.94    | 0.91    | 0.68    |
| **MutPred-Indel**      | 516    | 72     | 2116   | 1211   | 3915(98.8)   | 0.3     | 0.97     | 9.08$   | 0.73    | 0.88    | 0.64    | 0.81    | 0.37    |
| **MutationTaster2021** | 1675   | 99     | 1976   | 36     | 3786(95.5)   | 0.98    | 0.95     | 20.52$  | 0.02$   | 0.94    | 0.98    | –       | 0.93    |
| **PROVEAN**            | 1482   | 581    | 1470   | 82     | 3615(91.2)   | 0.95    | 0.72     | 3.35+   | 0.07$   | 0.72    | 0.95    | 0.93    | 0.66    |
| **SIFT-Indel**         | 1406   | 827    | 1287   | 313    | 3833(96.7)   | 0.82    | 0.61     | 2.09    | 0.30+   | 0.63    | 0.8     | –       | 0.43    |
| **VEST-indel**         | 1560   | 385    | 1758   | 179    | 3882(98.0)   | 0.9     | 0.82     | 4.99+   | 0.13+   | 0.8     | 0.91    | 0.93    | 0.71    |
| **VVP**                | 1720   | 728    | 1481   | 20     | 3949(99.6)   | 0.99    | 0.67     | 3.00+   | 0.02$   | 0.7     | 0.99    | 0.87    | 0.67    |

### DDD subset (70 pathogenic; 81 benign) 
| **Tool**               | **TP** | **FP** | **TN** | **FN** | **Total(%)** | **Sns** | **Spec** | **LR+** | **LR-** | **PPV** | **NPV** | **AUC** | **MCC** |
|------------------------|--------|--------|--------|--------|--------------|---------|----------|---------|---------|---------|---------|---------|---------|
| **CADD**               | 45     | 16     | 65     | 25     | 151(100)     | 0.64    | 0.8      | 3.25+   | 0.45    | 0.74    | 0.72    | 0.78    | 0.45    |
| **CAPICE**             | 64     | 44     | 37     | 6      | 151(100)     | 0.91    | 0.46     | 1.68    | 0.19+   | 0.59    | 0.86    | 0.82    | 0.41    |
| **FATHMM-indel**       | 66     | 38     | 43     | 4      | 151(100)     | 0.94    | 0.53     | 2.01    | 0.11+   | 0.63    | 0.91    | 0.74    | 0.51    |
| **MutPred-Indel**      | 17     | 16     | 64     | 53     | 150(99.3)    | 0.24    | 0.8      | 1.21    | 0.95    | 0.52    | 0.55    | 0.64    | 0.05    |
| **MutationTaster2021** | 50     | 19     | 61     | 19     | 149(98.7)    | 0.72    | 0.76     | 3.05+   | 0.36+   | 0.72    | 0.76    | –       | 0.49    |
| **PROVEAN**            | 60     | 32     | 45     | 6      | 143(94.7)    | 0.91    | 0.58     | 2.19    | 0.16+   | 0.65    | 0.88    | 0.86    | 0.51    |
| **SIFT-indel**         | 60     | 39     | 41     | 10     | 150(99.3)    | 0.86    | 0.51     | 1.76    | 0.28+   | 0.61    | 0.8     | –       | 0.39    |
| **VEST-indel**         | 62     | 29     | 51     | 8      | 150(99.3)    | 0.89    | 0.64     | 2.44+   | 0.18+   | 0.68    | 0.86    | 0.87    | 0.53    |
| **VVP**                | 68     | 70     | 11     | 2      | 151(100)     | 0.97    | 0.14     | 1.12    | 0.21+   | 0.49    | 0.85    | 0.64    | 0.19    |



## VEST-indel
The latest downloadable release is VEST 3.0. Last updated on 05/01/2014.

VEST 4.0 is the most recent version, but is only available trough the CRAVAT 5.0 server web application.

CRAVAT 5.0 server send back results via email a couple hours later for an exome VCF.

### output 
See [VEST's output](./outputs/VEST/)
- Gene_Level_Analysis.Result.tsv
- manual_input.txt.CRAVAT_analysis.dev.euphrasie_servant_20230308_050215.xls: .xls file with results
- Variant.Result.tsv
- Variant_Additional_Details.Result.tsv
- Variant_Non-coding.Result.tsv
- [Interactive viewer](http://www.cravat.us/CRAVAT/job_detail.html?job_id=euphrasie_servant_20230308_050215)

## CAPICE
- Was very complicated to set up 
- The VCF files need to be annotated with some VEP specific annotations
- Also functionnate as a VEP plugin!
  
### output 
A .tsv file with the following columns, for all variants. One line per ENST id: 

| chr  | pos    | ref | alt | gene_name | gene_id         | id_source | feature         | feature_type | score     | suggested_class |
|------|--------|-----|-----|-----------|-----------------|-----------|-----------------|--------------|-----------|-----------------|
| chr1 | 906272 | A   | C   | C1orf170  | ENSG00000187642 | HGNC      | ENST00000341290 | Transcript   | 0.5000117 | VUS             |

see [file](./outputs/CAPICE/capiceo.tsv)


## CADD 
- Included in VEP annotations. See CADD column in exomes' xlsx files.

## SIFT-indel 
- No CLI
- Limited to 100 variants per query.

## VPP 
- Has not been updated for 6 years.