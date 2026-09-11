# Module 1.2.3: Pre-processing

Once molecular data is translated into a digital form by a sequencer or mass spectrometer, it undergoes a series of computational processing steps to prepare it for analysis. The data are processed using computational and statistical methods to evaluate data quality, identify and quantify features, and reduce technical variation before addressing the biological question. Not every step will apply to every platform and the order of pre-processing steps and choice of methods matters.

Additionally, these decisions are not neutral. A filtering threshold determines which features enter downstream analysis; excluded features can be recovered only by repeating preprocessing from retained raw or intermediate data. A normalisation method based on assumptions that do not hold can distort downstream comparisons, while an imputation strategy that ignores why values are missing can introduce bias. The choice of genome assembly, gene annotation or protein database determines which features the pipeline can identify. Reads or signals that do not match the selected reference will not contribute to that analysis, although they may be recovered by reprocessing with another reference or method.

Across platforms, preprocessing commonly involves four broad types of task:

| Stage | Purpose | Genome | Transcriptome | Proteome | Metabolome | Epigenome | Microbiome |
|---|---|---|---|---|---|---|---|
| **Quality control** | Identify data quality issues before analysis | Sequence quality, read length distribution | Mapping rate, rRNA fraction | Signal-to-noise ratio, identification rates | TIC stability, QC pool reproducibility | Detection p-values, conversion rate | Read depth, primer removal |
| **Data cleaning** | Remove low-quality observations and noise | Low-quality read removal, adapter trimming | Adapter trimming, low-quality read removal | Peak picking, blank subtraction | Feature filtering, solvent blank removal | Failed probe removal | Chimera filtering, host read removal |
| **Reconstruction** | Infer the original biological sequence or structure | Read mapping to reference genome | Read mapping to transcriptome | Peptide-to-protein mapping | Feature annotation against spectral libraries | Read mapping to reference genome | OTU/ASV clustering |
| **Feature identification** | Annotate biologically relevant features | Variant calling | Gene quantification | Protein quantification | Metabolite identification | Methylation calling | Taxonomic assignment, abundance estimation |

??? note "Key terms"
    | Term | Definition |
    |---|---|
    | **Quality control (QC)** | Assessment of raw data to identify samples or features that fail technical thresholds — low sequencing depth, poor alignment rate, high duplicate rate, degraded signal |
    | **Filtering** | Removal of features (genes, proteins, taxa, metabolites) that do not meet a minimum threshold of detection or prevalence across samples |
    | **Missingness** | The absence of a measured value for a feature in one or more samples; can arise from true absence, signal below the detection threshold, or technical failure |
    | **Imputation** | Estimating a missing value from the values that are present, using statistical or data-driven methods |
    | **Normalisation** | Adjustment of measured values to reduce systematic technical differences in scale or distribution such as differences in sequencing depth, sample loading or instrument sensitivity that could obscure biological differences.|

!!! tip "Always keep your raw files!" 
    Many preprocessing decisions can be revised by rerunning the pipeline, provided that the raw data have been retained. Raw data, reference versions, software versions, parameters and filtering decisions should therefore be preserved and documented.

## Consideration 6: Data quality and cleaning

!!! danger "Design principle"
    QC criteria should be planned in advance where possible. When thresholds are informed by the observed QC distributions, the rationale should be documented and applied consistently. Thresholds should not be adjusted based on condition labels or desired results.

### Quality control 

Raw data always contains observations of variable quality. Quality control is the process of: 

- Systematically evaluating the data before analysis
- Identifying samples that have failed partially during collection or processing
- Assessing whether the instrument or sequencing run performed consistently
- Checking that individual features meet a minimum standard of detection. 

Each of these can introduce a different kind of problem: a failed sample adds noise or outliers to group comparisons; a drifting instrument introduces a run-wide trend that affects every measurement; features indistinguishable from background inflate the apparent size of the dataset without contributing signal. Addressing them requires different decisions. These problems require different checks and should be assessed before downstream analysis. QC should also be revisited after major filtering or normalisation steps.

| Omics domain | Platform | QC metric | What an unusual value may suggest |
|---|---|---|---|
| Genome | WGS / WES | Coverage depth and breadth | Insufficient or uneven sequencing, leaving parts of the genome inadequately measured |
| Genome | WGS / WES | Duplication rate | Low library complexity, limited input material or excessive PCR amplification |
| Genome | WGS / WES | Cross-sample contamination estimate | Mixture of material from different samples or possible sample-handling errors |
| Transcriptome | Bulk RNA-seq | Number of mapped reads | Insufficient usable sequencing depth |
| Transcriptome | Bulk RNA-seq | Mapping rate | Poor read quality, contamination or an unsuitable reference genome or annotation |
| Transcriptome | Bulk RNA-seq | Proportion of reads mapping to rRNA | Incomplete rRNA depletion, RNA degradation or low informative RNA content |
| Transcriptome | Single-cell RNA-seq | Proportion of mitochondrial reads per cell | Damaged or dying cells, although expected levels differ among tissues and cell types |
| Proteome | LC-MS/MS | Number of proteins identified per sample | Low sample input, sample-preparation problems, poor injection or reduced instrument performance |
| Proteome | LC-MS/MS | Total ion current (TIC) | Differences in sample loading, injection, ionisation or instrument sensitivity |
| Metabolome | LC-MS / GC-MS | CV of feature intensities across pooled QC injections | Analytical variability, instrument drift or inconsistent injection |
| Metabolome | LC-MS / GC-MS | Signal-to-blank ratio | Signal may reflect background contamination rather than a sample-derived feature |
| Microbiome | 16S / metagenomics | Read count per sample | Low library yield, low microbial biomass or insufficient sequencing depth; contamination may dominate low-biomass samples |
| Microbiome | 16S / metagenomics | Chimeric sequence rate | PCR amplification artefacts that may inflate apparent diversity |
| Epigenome | DNA methylation arrays | Detection p-value per probe | Probe signal cannot be reliably distinguished from background |
| Epigenome | Bisulfite sequencing | Bisulfite conversion efficiency | Incomplete conversion may cause unmethylated cytosines to be incorrectly called as methylated |

QC metrics should be interpreted together and in the context of the platform, sample type, controls and overall data distribution. Comparisons across samples also require consistent acquisition and processing settings. For example, protein-identification counts are comparable only when the same acquisition mode, database-search settings and identification thresholds were used.

### Filtering 

Filtering is related to, but distinct from, quality control. QC identifies potential quality problems; filtering applies defined criteria to remove low-quality samples, observations or features. A protein quantified in only 2 of 80 samples may provide too little information for reliable estimation, while a metabolite whose signal cannot be distinguished from the solvent blank may represent background rather than biological signal. Similarly, microbiome taxa represented by a single read across the entire dataset are commonly removed.

The risk in filtering is that low-prevalence or low-abundance features are not necessarily biologically unimportant. A taxon present in 15% of cases and absent from all controls would be removed by a standard 20% prevalence threshold and with it, the only organism differentiating the two groups. A protein consistently detected at low abundance in one condition and absent in another, may carry relevant differential information, although the pattern must be evaluated against detection limits and possible technical missingness. The appropriate threshold depends on the platform, the sample size, and what the study is designed to detect. It should be chosen with the biological question in mind, not inherited from a pipeline default.

### Missingness

Missingness is the absence of a measured value for a feature in one or more samples. A value can be absent because the feature was genuinely not present in the sample, because it was present but fell below the instrument's detection threshold, or because of a technical failure during processing. These situations are not equivalent and should not be handled the same way.

The key question is why values are missing and whether the pattern is related to feature abundance, sample quality, batch or biological condition. Missingness caused by random technical failures differs from missingness caused by a detection limit or a systematic processing problem, and these mechanisms may require different approaches. A feature consistently unrecorded in one condition and measured in another may reflect biology, detection limits, batch allocation or sample processing. This pattern should therefore be investigated before deciding whether imputation is appropriate.

The proportion of missingness also matters. A feature missing in the majority of samples in one group cannot be reliably estimated from the few values that exist. Whether it should be imputed, treated as absent, or excluded from the analysis depends on the platform and the question being asked, but the decision should be explicit, not left to a pipeline default.

### Normalisation

Measured values in omics data reflect both biological signal and technical variation. Two samples may produce different read counts, protein intensities, or metabolite peak areas not because the biology differs, but because one sample had more input material, was processed on a different day, or was run on the instrument at a different position in the queue. Normalisation adjusts for systematic technical differences in measurement scale or distribution so that samples can be compared more fairly. It does not necessarily remove batch effects or other structured technical variation.

The appropriate method depends on the platform and the assumptions that hold for the dataset. In RNA-seq, normalisation commonly accounts for differences in library size and composition. In proteomics, methods such as median centring or total-intensity scaling can adjust for differences in overall signal between samples. In metabolomics, appropriate internal standards added before extraction can help monitor and adjust for specific sources of technical variation. Standards and spike-ins must therefore be introduced before the processing step they are intended to monitor.

Some normalisation strategies assume that most features are unchanged between conditions. This assumption is violated when the biological effect is global — for example, a transcriptional shutdown affecting the majority of genes, or a metabolic phenotype characterised by broad shifts in abundance across many metabolites. In such cases, normalisation to a stable reference set or to spike-ins is more appropriate than methods that anchor to the dataset's own central tendency.

--- 

!!! info "Stage C takeaways"
    - Preprocessing transforms raw instrument output into a form suitable for analysis. The steps involved vary by platform, and the order and choice of methods affect what information enters the analysis.
    - QC should assess sample quality, run or instrument performance, and feature-level detection. QC criteria should be planned where possible, applied consistently and documented.
    - Filtering removes low-quality or low-prevalence features, but low abundance does not mean biologically unimportant. Thresholds should reflect the biological question, not pipeline defaults.
    - Missing values arise for different reasons and the appropriate response differs in each case. Structured missingness may reflect biological or technical processes and should be investigated before imputation.
    - Normalisation adjusts for selected sources of technical variation and relies on assumptions about the data. Reference materials and spike-ins must be introduced before the processing steps they are intended to monitor.
    - The choice of reference database or genome assembly determines what can be detected. Outdated or mismatched references may exclude, misidentify or misannotate features.
