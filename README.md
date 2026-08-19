# BIO101 - Design foundations for omics studies

Omics technologies are now routine tools across the life sciences. Most omics training focuses on downstream data analysis, how to process sequencing data, perform differential expression analysis, or use specialized software. While these skills are essential, they often come too late. Many of the factors that determine whether an omics study produces meaningful, interpretable results are decided before a single sample is processed.

In this workshop, you will learn the basics of study design for bioinformatics-based research. Through real world examples, you’ll explore the main omics data types and how they differ from conventional biological data, identify key decision-making steps during a full experimental workflow, and show how decisions at each stage propagate into your results. Working through these principles, you will be better equipped to design robust bioinformatics experiments, critically evaluate the design of others, and avoid the mistakes that downstream analyses cannot fully fix.

## Developers 

- Amarinder Thind 
- Georgie Samaha 
- Fred Jaya 
- Mitchell O'Brien

## Format

This is a full-day, in-person only, interactive workshop combining short presentations, real-world case studies, group discussions, and hands-on activities. It will be held in Room 503 Moore College (CG2), 1 King Street, Newtown, NSW, 2042.

Who the workshop is for: This workshop is aimed at those coming to bioinformatics from a clinical or biology background who are comfortable with biology but new to design and statistical thinking required for omics data analysis. No prior bioinformatics, coding, or statistics experience is required.

## Prerequisites

- A basic understanding of biological research concepts
- Participants should bring a laptop for browser-based practical activities (no software installation required)

## For developers 

To render docs: 

1. Install mkdocs

```
pip install mkdocs
mkdocs --version # confirm install
```

2. Render docs locally at http://127.0.0.1:8000/: 

```
mkdocs serve
```

All content merged to main will be rendered at github.io pages by [`.github/workflows/mkdocs_deploy.yml`](.github/workflows/mkdocs_deploy.yml) github action.