# Module 1.2: Experimental workflow activity

You have worked through five stages of an omics study and ten considerations that shape what a dataset can support. Apply them to your own study.

!!! question "Activity: your study across the workflow"

    1. **Map your study across the five stages. At which stage are your decisions most constrained. It can either already fixed, or hardest to revise?**

    2. **Identify the two considerations that pose the greatest risk to your conclusions. What would need to be true for those risks not to matter?**

    3. **What would a reader need to know to reproduce your analysis and evaluate whether your findings are generalisable?**

    ??? example "Clinical / human disease"

        *A cardiac biomarker study processed cases in 2022 and recruited controls from a public dataset in 2024. Differential proteins were identified and reported as candidate biomarkers.*

        Consider: batch and biology are now confounded — what can the data actually support? The public controls introduce unknown processing differences. The finding is from a single cohort with no independent replication. Which of the ten considerations apply, and what would need to change for the conclusions to hold?

    ??? example "Wildlife / infectious disease"

        *A microbiome study collected cloacal swabs from diseased and healthy individuals across three field sites over two seasons. Samples were processed in two batches by two operators.*

        Consider: site, season, operator, and batch are all potential confounders. Which are recorded as metadata? Which could be modelled, and which are unrecoverable? If the diseased animals came disproportionately from one site, what does the data actually show?

    ??? example "Aquaculture / production biology"

        *A transcriptomics study of fast- and slow-growing fish took three tissue biopsies per individual and treated each biopsy as an independent replicate, giving n=30 per group from 10 fish per group.*

        Consider: the experimental unit is the fish, not the biopsy. What is the true n? If batch aligns with growth rate — fast growers processed first — can the biological signal be separated from the technical? What metadata would allow you to assess this retrospectively?

    ??? example "Plant / environmental stress"

        *A metabolomics experiment measured 600 metabolites across 12 stressed and 12 control plants. Results were reported as significant at p < 0.05 with no multiple-testing correction. No spectral library version or software parameters were recorded.*

        Consider: at p < 0.05 across 600 features, how many findings are expected by chance? What does FDR correction do to the result list? Without software version and parameters, what can another lab reproduce? At which stage did the key decisions happen, and which are now irreversible?
