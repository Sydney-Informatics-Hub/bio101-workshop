# Module 1.2.4: Analysis

Analysis is the stage at which statistical models are applied to the preprocessed datasets to test the biological question. The model must reflect the structure of the data: the types of variables, the distributional properties of the outcome, any dependencies between observations, and covariates that need to be accounted for. A model that correctly captures these properties produces estimates with appropriate uncertainty; one that does not can overstate confidence or fail to detect real effects.

Analysis in omics is characterised by two challenges that require explicit design decisions. First, thousands of molecular features are tested simultaneously. Testing at this scale increases the expected number of false positives proportionally — at p < 0.05 across 20,000 features, approximately 1,000 significant results are expected by chance alone. Multiple-testing correction reduces this risk but does not eliminate it; computational approaches such as permutation testing can further assess how extreme the observed results are relative to chance. Second, observations in omics data are frequently not independent: cells from the same donor, repeated measurements from the same individual, or subsamples from the same tissue share a common biological background. Treating them as independent replicates inflates the effective sample size and overstates confidence in the results.

Both of these are addressed directly in the considerations below.

## Consideration 7: Experimental and analytical controls

!!! danger "Design principle"

    Experimental controls help assess the measurement process. Analytical controls help assess the reliability of the analysis. Both are needed as analytical controls cannot reliably replace missing experimental controls.

Analytical controls are not a substitute for experimental controls. Where experimental controls (negative controls, spike-ins, technical replicates) assess whether the measurement process itself was reliable, computational controls can be used to assess whether analytical results are more extreme than expected by chance, or whether identifications meet a minimum confidence threshold.

In proteomics, decoy databases (constructed from reversed or randomised protein sequences) are searched alongside the real database. Because a match to a decoy sequence cannot be biologically real, the rate at which decoys are matched gives an empirical estimate of the false discovery rate among the real identifications. 

Permutation tests assess how unusual the observed result would be if there were no association between the groups and the measurements. They rearrange group labels and repeat the analysis to see how often a result at least as extreme occurs. The rearrangement must respect the study design, including pairing or repeated measurements.

??? example "Case study: The placental microbiome"

    Some studies reported a resident community of microorganisms in the
    placenta. However, the amount of microbial DNA detected in placental
    samples is typically very low, making their sequencing results
    particularly vulnerable to contamination.

    Later investigations using extensive controls found no evidence of a
    resident placental microbiome. Much of the detected bacterial DNA was
    attributable to contamination introduced during sample collection or
    laboratory processing. This does not mean that bacteria can never be
    present: occasional pathogens are different from a resident microbial
    community.

    **Why experimental controls matter**

    A negative extraction control contains no tissue but passes through the
    same extraction workflow as the samples. Bacterial DNA detected in these
    controls helps identify contamination from reagents or processing.
    Comparing samples with controls helps assess whether the signal supports
    a biological interpretation.

    This illustrates a limit of computational analysis: detecting bacterial
    sequences does not, by itself, establish that those bacteria originated
    in the tissue.

    <small>
    de Goffau MC et al. Human placenta has no microbiome but can contain
    potential pathogens. *Nature* 572, 329–334 (2019).
    [doi:10.1038/s41586-019-1451-5](https://www.nature.com/articles/s41586-019-1451-5){target="_blank"}

    Salter SJ et al. Reagent and laboratory contamination can critically
    impact sequence-based microbiome analyses.
    *BMC Biology* 12, 87 (2014).
    [doi:10.1186/s12915-014-0087-z](https://link.springer.com/article/10.1186/s12915-014-0087-z){target="_blank"}
    </small>

!!! danger "What analysis cannot fix"

    Analysis cannot reliably compensate for missing experimental controls or
    essential information that was never collected. Sometimes the impact can
    be assessed or partially mitigated, but resolving the uncertainty may
    require additional measurements or a new experiment.
---

## Consideration 8: Independent replication and pseudoreplication

!!! danger "Design principle"
    Statistical inference should be performed at the level of the experimental unit, not the observational unit. Treating multiple measurements from the same experimental unit as independent replicates inflates the effective sample size and overstates confidence in the results.

As introduced earlier, several measurements may come from the same
biological unit. Multiple biopsies or cells from one patient provide more
information about that patient, but do not increase the number of
independent patients studied.

Treating these measurements as independent biological replicates is
**pseudoreplication**. The analysis must account for their shared origin.

Two design choices require particular care when counting independent replicates: subsampling and pooling.

- **Subsampling** means measuring several parts of the same biological unit, such as multiple cells from one donor or multiple biopsies from one patient. These measurements provide more information about that individual, but they do not increase the number of independent individuals studied. The analysis must account for their shared origin.

- **Pooling** Pooling combines material from several biological units into one measured sample. For example, combining samples from five donors into one pool produces one pooled measurement, not five separate donor measurements. Individual differences can no longer be directly assessed from that measurement. Replication depends on how many independent pools were created and how they were constructed.

Neither subsampling nor pooling is inherently a mistake. Pseudoreplication occurs when subsamples are treated as independent biological replicates, or when donors contributing to a pool are counted as separately measured replicates. This can overstate confidence in the results. Dependence between subsamples can often be handled in the analysis, but pooling generally prevents direct assessment of individual differences.

!!! info "Multiplexing is not pooling"
    Multiplexing combines separately barcoded libraries onto the same sequencing run for efficiency. Demultiplexing recovers separate library measurements; whether these represent independent biological replicates depends on the study design. Samples from ten independent patients run together on one lane still represent ten independent biological units. Pooling biological material generally prevents separate measurement of individual contributions, unless these remain distinguishable through genetic differences or other identifiers.

**Pseudoreplication in single-cell RNA-seq**

Unlike bulk RNA-seq, which measures average gene expression across thousands of cells, single-cell RNA-seq profiles each cell individually, capturing the variation that bulk methods average away. A single experiment can generate profiles for tens of thousands of cells from a handful of donors. This resolution comes with a statistical trap: cells from the same individual share a common genetic and environmental background — they are subsamples of that individual, not independent observations. Analysing them as independent replicates inflates the degrees of freedom and elevates the false positive rate.

![](figs_m1/03_pseudoreplication_single_cell_v02.jpg){width=95%}

??? example "Case study: Pseudoreplication in single-cell omics"
     The study profiled approximately 80,000 nuclei from 48 individuals and
    included both cell-level testing and a patient-level analysis. Using the
    same processed data, a reanalysis compared the original cell-level results
    with pseudobulk analysis, aggregating counts within each donor and cell type.
    At FDR < 0.05, unique differentially expressed genes fell from 14,274 to 26.
    Fewer discoveries alone do not prove false positives. However, randomly
    reassigning patient labels still produced many discoveries with cell-level
    testing, a pattern not seen with pseudobulk analysis.

    ![](figs_m1/01pseudoreplication__case_study_v02.png){width=100%}

    <small>Original study: [Mathys et al. "Single-cell transcriptomic analysis of Alzheimer's disease." *Nature* 570 (2019)](https://www.nature.com/articles/s41586-019-1195-2){target="_blank"}</small>

    <small>Reanalysis: [Murphy et al. "Avoiding false discoveries in single-cell RNAseq by revisiting the first Alzheimer's disease dataset." *eLife* 12 (2023)](https://elifesciences.org/articles/90214){target="_blank"}</small>

---

!!! info "Module 1.2.4 takeaways"
    - Studies that lack appropriate experimental controls may be uninterpretable regardless of the analysis applied.
    - Multiple measurements from the same experimental unit must not be
    counted as independent replicates. The analysis can summarise measurements
    within each unit or use a model that accounts for their dependence.
    - Subsampling and pooling require careful counting of independent replicates. More measurements or more donors contributing to a pool do not necessarily mean more independent replicates. 
    - Multiplexing preserves sample identity. Whether samples represent independent biological replicates depends on the study design.

