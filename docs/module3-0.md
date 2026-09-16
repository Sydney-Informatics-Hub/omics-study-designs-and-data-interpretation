# Module 3: Diagnosing design problems in omics

!!! info "Learning objectives"
    - Apply diagnostic thinking across different data types and experimental design elements
    - Assess whether experimental limitations can be addressed through analysis or require redesign

In Module 1 and Module 2, we looked at the omics layers, the key design considerations, and the trade-offs between accuracy, interpretability, power, cost, and generalisability. Module 3 brings those ideas together by asking how to diagnose whether a study is asking the right question, measuring the right thing, and designing around the right constraints.

## Recap: a mental model checklist

| Criterion | Question | Considerations |
|---|---|---|
| **Molecular model fit** | Is the chosen molecular layer appropriate for the biological question? | Which molecular layer best matches the biology being studied; what each omics layer captures and what it cannot tell you; whether the measurement is close to the biology of interest rather than a downstream or indirect readout. See [2.1.1 Choosing a measurement platform](module2-1-1.md). |
| **Interpretability** | Will the result mean what we think it means? | Confounding and batch effects; blocking and randomisation; normalisation appropriate to the data; tissue or cell composition; positive and negative controls; statistical versus biological significance. See [2.1.2 Confounding: when a variable travels with your groups](module2-1-2.md) and [2.1.3 Measurement reliability and metadata](module2-1-3.md). |
| **Metadata completeness** | Is the study documented well enough for others to interpret and reproduce it? | Sample metadata such as age, sex, tissue, disease status, collection site, timing, and processing conditions; batch identifiers; storage, handling, and instrument metadata; knowing which variables are missing and how those gaps affect interpretation. See [2.1.3 Measurement reliability and metadata](module2-1-3.md). |
| **Signal detection** | Can the design detect the effect we care about? | Statistical power given the correct error model; multiple-testing burden; the unit of replication; missingness or dropout reducing effective sample size; whether the study was designed around the size of effect it intends to detect. See [2.2.1 Sample size and statistical power](module2-2-1.md). |
| **Resource use** | Is the budget being used effectively? | Sequencing depth versus breadth; technical versus biological replication; budgeting for QC attrition; platform cost versus the needs of the research question. See [2.2.2 Design decision costs](module2-2-2.md). |
| **Generalisability** | Will the results hold outside our dataset? | Cohort representativeness versus the target population; whether results hold across different omics data types; reference and annotation bias; whether independent validation is possible. See [2.3.1 Generalisability: who and what the findings apply to](module2-3-1.md). |
| **Design coherence** | Are the scientific question, cohort, variables, and platform aligned before data are generated? | Clear biological question; explicit hypothesis; well-defined comparison groups; relevant covariates and confounders; a platform that can answer the question within the study's cost and time constraints; a realistic statement of what the design can and cannot support. See [2.4.1 Design decisions in practice](module2-4-0.md). |

---

!!! tip "Next step"
    Start with [Module 3.1: Introduction and case studies](module3-1.md), then continue to [Module 3.2: Activity outline and exact steps](module3-2.md).
