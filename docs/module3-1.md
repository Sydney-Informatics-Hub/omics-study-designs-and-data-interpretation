# Module 3.1: Activity and case studies

!!! info "Learning objectives"
    - Diagnose whether a study design matches the biological question being asked
    - Identify confounding, batch structure, and generalisability issues in omics studies
    - Decide whether a limitation can be handled through analysis or requires redesign

This module is designed as a practical exercise in study diagnosis. The goal is to look at a study design, decide what the main comparison is, and then ask whether the design actually supports the research outcome.

## Activity

!!! question "Diagnose a study"
    1. Pick one scenario from the list below:
        - [Scenario A: Proteomics in an acute inflammatory condition](#scenario-a-proteomics-in-an-acute-inflammatory-condition)
        - [Scenario B: Genomic markers for breed traits in dogs](#scenario-b-genomic-markers-for-breed-traits-in-dogs)
        - [Scenario C: Single-cell RNA sequencing in inflammatory disease](#scenario-c-single-cell-rna-sequencing-in-inflammatory-disease)
    2. Look at the study and use the [omics calculator](https://sydney-informatics-hub.github.io/omics-calculator/) to explore how design choices, sample size, and measurement choices affect what the study can detect.
    3. Use the ideas from the day to answer the [practical questions](#the-practical-questions-to-answer) about the study design.
    4. Be creative. There are no single right answers. Think about validation studies, follow-up studies, redesigns, or alternative study structures that could support your reasoning.

    Study design is hard to master, and some limitations are outside our control. Think big, challenge the design, and explain why you think the findings are or are not trustworthy.

------------------------------------------------------------------------

### Scenario A: Proteomics in an acute inflammatory condition

#### Study question

Are there protein-level differences in circulating blood associated with acute nephritis in young patients, relative to controls without the condition?

**Omics type:** Mass spectrometry proteomics, data-independent acquisition

#### Study design

Cases were recruited prospectively at admission to hospital for nephritis and deliberately stratified into three roughly equal age groups to spread age evenly across the case group. Controls were assembled opportunistically from an existing sample biobank. There was no matched recruitment protocol running alongside case collection. Both groups are heavily skewed toward one sex and younger ages.

??? note "What do the columns in the data mean?"
    For Study A, the columns are:

    - Sample: unique identifier for each participant
    - Age: age in years
    - Sex: biological sex of the participant
    - Disease status: whether the participant has the disease or is a control
    - Age group: age category used to balance or stratify the study (yound, mid, old)
    - outcome: whether the participant had a complication, recovered after the initial event or were never affected (contols)
    - Renal function: measure of kidney function, such as creatinine or eGFR
    - BMI: body mass index, a measure of body size



------------------------------------------------------------------------

### Scenario B: Genomic markers for breed traits in dogs

#### Study question

Can we identify genomic variants associated with observable traits across dog breeds using public data from unrelated studies?

**Omics type:** Whole genome sequencing

#### Study design

Whole genome sequencing data from 500 dogs across 134 breeds were aggregated from multiple public archives. No individual-level phenotypic measures were available other than reported breed identities. Phenotypic data were then constructed by reporting the median score for breeds using standards published by the American Kennel Club. Quantitative traits were labelled with a raw median value from the AKC, while binary traits were coded as 1 for trait present and 2 for trait absent.

??? note "What do the columns in the data mean?"
    For Study B, the columns are:

    - Sample: unique identifier for each dog
    - Breed: dog breed
    - Sex: Biological sex of sample male or female
    - *Weight: body weight
    - *Height: body height or shoulder height
    - *Life span: expected lifespan 
    - *Long legs: presence or absence for long leggedness
    - *Drop ears: presence or absence for dropping ear shape
    - *Large ears: presence or absence for large ears
    - *Tail curl: presence or absence for tail curl 
    - *Bulky: presence or absence for observed bulking in body shape
    - *Muscled: presence or absence for muscularity in body shape
    - *White chest: presence or absence of white chest markings in coat colour
    - *White head: presence or absence of white head markings in coat colour
    - *Hairless: whether the dog is hairless or not
    - *Length of fur: presence or absence of long fur
    - *Furnish: presence or absence of coat texture or furnishings
    - *Boldness: behavioural trait score
    - *Aggressiveness: behavioural trait score

    *these are average scores as indicated by breeding standards.

This scenarios is based on real data published [here](https://www.nature.com/articles/s41467-019-09373-w). After answering your questions you can see how the authors dealt with percieved design flaws.



------------------------------------------------------------------------

### Scenario C: Single-cell RNA sequencing in inflammatory disease

#### Study question

Can we identify differentially expressed genes across individual cell types in healthy individuals versus individuals presenting a pro-inflammatory condition?

**Omics type:** Single-cell RNA sequencing

#### Study Design

Single-cell RNA sequencing was collected from blood samples and enriched for circulating immune cells. Donors consist of two healthy individuals in the control group and two individuals presenting pro-inflammatory disease symptoms. The single-cell RNA sequencing data has undergone QC, preprocessing, and annotation for a total of 18 cell subtypes across T cells, natural killer cells, monocytes, and dendritic cells.

??? note "What do the columns in the data mean?"
    For Study C, the columns are:

    - Sample_id: unique identifier for each sample
    - donor_id: unique identifier for the individual donor
    - condition: study group, case versus control
    - hospital_referral: identifier for hospital that referred patient for testing
    - ancestry: self reported genetic ancestry
    - sex: biological sex of the donor
    - age: donor age
    - tissue: tissue source of the sample
    - processing_date: date samples were processed
    - n_cells: number of cells in that cell type 

------------------------------------------------------------------------

## The practical questions to answer

For each scenario, answer the questions below. Use the hints to guide your thinking, but do not treat them as a checklist with only one correct answer.

### 1. Identify the comparison

What is the main comparison being made, what omics type is used, and does this answer the research question well?

??? tip "Hint"
    Does the omics layer relate well to the biological variable being studied? Are you measuring the molecule or process that actually drives the trait, or only a downstream readout? Does the data type match the scientific question?

### 2. Look for confounders

Are there variables that differ between groups that could affect the outcome?

??? tip "Hint"
    Were any variables clearly different between groups and could they act as confounders? Consider sex, age, disease severity, ancestry, treatment, collection time, or cell type composition. Ask whether each variable is part of the biology being studied or a design artefact that could bias the result. If it is a confounder, what direction or pattern of bias might it create?

### 3. Check technical structure

Could batch or technical effects influence the results, and were they captured?

??? tip "Hint"
    Were samples processed together or across separate batches, sites, runs, or operators? Were technical covariates recorded, such as instrument, run date, reagent batch, extraction batch, or sample quality metrics? If a technical effect is present, could it be mistaken for biology?

### 4. Define the scope of the findings

Could these findings apply to populations outside this study?

??? tip "Hint"
    Think about scope and generalisability. Are the conclusions limited to a particular sex, ancestry, species, tissue, cell type, disease stage, or setting? Can the finding reasonably be applied beyond the exact study population, or are the results only valid for a narrower group?

### 5. Propose an improvement

How would you improve the design?

??? tip "Hint"
    Is the main problem a mismatch between the omics layer and the biology, confounding that could be prevented by better matching or blocking, unrecorded metadata, poor batch control, or a study population that is too narrow? Consider whether the issue can be addressed analytically or whether the design itself needs to change.



------------------------------------------------------------------------

## What to take away

Across these scenarios, the same design logic applies:

- The platform must match the biology being asked.
- The groups being compared must be reasonably comparable.
- Technical structure must be considered and, where possible, controlled.
- The scope of the inference must match the study design.
- If a limitation cannot be fixed analytically, improve the design itself or validate the conclusions with a better-supported follow-up study.
