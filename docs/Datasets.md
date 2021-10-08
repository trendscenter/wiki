---
layout: default
title: Datasets
nav_order: 2
parent: Storage Guide
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Neuromark

Clinical similarities among brain disorders have been recognized for
many decades. Although some brain disorders are now recognized as
distinct diseases, they share overlapping genetic etiology, common
abnormalities in brain function and structure, and similar cognitive
impairments, confounding the diagnosis and treatment plans.
Neuroimaging, a more specific and biologically based approach for
detecting brain changes, has advanced our knowledge of disease-related
brain dysfunction and provided reliable biomarkers for clinical usage in
some cases. However, previous studies typically focus on one or two
disorders only, ignoring the study of overlapping and unique brain
abnormalities among brain disorders. Characterizing brain changes across
disorders using neuroimaging approaches and understanding the
connections and relationships between them may shed light on etiologies
and aid in the deconstruction of psychiatric illnesses. Indeed, how to
compare biomarkers across multi-disorders and how to replicate
biomarkers are two critical issues which attract increasing
consideration in the neuroimaging research field. Region of interest
(ROI) based analysis and independent component analysis (ICA) are the
two most common approaches for exploring the functional organization of
the brain. While ROI based methods require fixed brain regions according
to prior experiences or knowledge from in-hand data, ICA, a data-driven
method with an assumption of independence between identified components,
is capable of capturing functional features retaining individual
variability. Our previous studies along with others have found that a
set of features derived from ICA can serve as potential biomarkers of
several brain disorders, with the ability to predict disease traits and
cognitive declines. However, unlike univariate methods, comparing
results obtained from different ICA runs is not so straightforward due
to the difference in the identified target components and their
arrangements, which greatly raises difficulty on examining results from
multiple studies and also decreases the possibility for the replication
of existing results. In this project, we aim to launch a novel unified
ICA framework which can be used to link multiple diseases, datasets, and
studies. The framework is capable of generating more accurate
individual-level functional networks as well as to identify the
correspondence of networks across subjects/datasets/studies, also useful
to evaluate replication. Based on this framework, comparable ICA
features, such as the spatial maps within functional networks and
functional (among) network connectivity, will be extracted from each
subject respectively. We will employ this framework using a database
created from a large sample healthy controls and individuals with
different brain disorders (schizophrenia, autism,
attention-deficit/hyperactivity disorder, and major depression
disorder). This database will be formed by combining data collected from
multiple open-source and our own datasets. It is expected that by using
this robust and generalized framework, disease overlap and divergence of
various ICA features can be quantified and summarized. The results might
help to provide credible evidence regarding the neural basis
contributing to the overlapping symptoms in brain disorders and thus
contribute to the understanding of the specificity of brain disorders as
well as their inter-relationships (such as continuously changing,
distinct, or common) among them.

**References**

\[1\] Y. Du et al., “NeuroMark: an automated and adaptive ICA based
pipeline to identify reproducible fMRI markers of brain disorders,”
NeuroImage: Clinical, p. 102375, Aug. 2020, doi:
[10.1016/j.nicl.2020.102375](http://doi.org/10.1016/j.nicl.2020.102375).

### Summary

\* Not preprocessed

Collaborative spreadsheet:
<https://drive.google.com/file/d/126Su7fBqaVAjefCe4s4Prk9qk_zdzsVy/view?usp=sharing>

| Name                           | fMRI                                             | sMRI                                             | dMRI                                              | SNIP | Groups                           |
|--------------------------------|--------------------------------------------------|--------------------------------------------------|---------------------------------------------------|------|----------------------------------|
| BSNIP                          | 1354                                             | 1354                                             |                                                   | 628  | HC, SZ, BP, Relatives            |
| FBIRN                          | 368                                              | 368                                              |                                                   | 278  | HC, SZ                           |
| COBRE                          | 204                                              | 204                                              |                                                   | 226  | HC, SZ, BP                       |
| Peter Kochunov (U of Maryland) | 457                                              | 444                                              |                                                   | 1076 | HC, SZ                           |
| Chinese Schizophrenia dataset  | 1614                                             | 954                                              |                                                   |      | HC, SZ                           |
| UCLA-CNP                       | 261                                              | 261                                              | 261                                               |      | HC, SZ                           |
| Schizophrenia Johns Hopkins    | 180                                              | 180                                              |                                                   |      | HC, SZ                           |
| HCP early psychosis            | 169                                              | 169                                              | 169                                               |      | HC, early psychosis patients     |
| ABIDE1                         | 1112                                             | 1112                                             |                                                   |      | HC, ASD                          |
| ABIDE2                         | 1113                                             | 1113                                             | 318                                               |      | HC, ASD (some longitudinal data) |
| OSUCH                          | 103                                              | 156                                              |                                                   |      | HC, mood disorder                |
| ECT (UCLA & UNM ECT data)      | 180                                              | 180                                              |                                                   |      | HC, MDD (before & after ECT)     |
| Chinese Major depression data  | 600                                              | 590                                              |                                                   |      | HC, MDD                          |
| ADNI                           | 373                                              | 1625                                             | 383                                               |      | HC, AD, MCI, EMCI, LMCI          |
| STANFORD-ADRC                  | 204                                              | 204                                              |                                                   |      | HC, AD, MCI, LBD, PD             |
| MarkVCID                       | 97                                               | 20                                               | 5                                                 |      | HC, LA, AD, SIVD, Mixed dementia |
| OASIS Cross-Sectional          |                                                  | 436                                              |                                                   |      | HC, AD                           |
| OASIS Longitudinal             |                                                  | 373                                              |                                                   |      | HC, AD                           |
| OASIS3                         | 1691                                             | 2217                                             | 1205                                              |      | HC, AD, MCI                      |
| ADHD200                        | 949                                              | 949                                              |                                                   |      | HC, ADHD-C, ADHD-H/I, ADHD-I     |
| Suijing ADHD dataset           | 189                                              | 116                                              |                                                   |      | HC, ADHD                         |
| ADHD unknown                   | 197                                              | 197                                              |                                                   |      | HC, ADHD                         |
| Hutchison's substance use      | 989                                              | 989                                              |                                                   |      | Alcohol, Nicotine disorder       |
| Anees Neuroimage data          |                                                  | 6008                                             |                                                   |      | HC and other diseases            |
| GSP                            | 1182                                             | 1182                                             |                                                   |      | HC                               |
| HCP                            | 1115                                             | 1058                                             |                                                   |      | HC                               |
| ABCD                           | 11764 (before Release 2.0)                       | 11764                                            | 3976                                              |      | HC                               |
| UK-BIO Bank                    | 39342                                            | 41182                                            |                                                   |      | HC and self-reported diagnosis   |
| Total                          | 75405                                            | 6317                                             | 2563                                              |      |                                  |

## NDAR

Follow the steps below to download data from
[NDAR](https://nda.nih.gov/).

-   Go to
    <https://nda.nih.gov/general-query.html?q=query=collections%20~and~%20orderBy=id%20~and~%20orderDirection=Ascending>
-   Select what you like to download
-   Add to filter (takes long time)
-   Create a package (also takes long time)
-   All data in the package can be downloaded using this Python package:
    <https://github.com/NDAR/nda-tools>
-   The preferred method for downloading scan data files is as follows:
    -   Download a package without associated data, e.g.
        `downloadcmd `<packageID>` -dp`
    -   Then extract the s3 locations from the downloaded image03.txt
        file, e.g. remain.txt

```
$ head remain.txt
s3://**************/submission_13124/NDARINVRP3R4YCP_baselineYear1Arm1_ABCD-rsfMRI_**************.tgz
s3://**************/submission_13124/NDARINVTAX3MN8C_baselineYear1Arm1_ABCD-rsfMRI_**************.tgz
s3://**************/submission_13124/NDARINVJ2ENP1ZK_baselineYear1Arm1_ABCD-rsfMRI_**************.tgz
s3://**************/submission_13124/NDARINVUKPZU1JW_baselineYear1Arm1_ABCD-rsfMRI_**************.tgz
s3://**************/submission_13124/NDARINV5VGKMHCR_baselineYear1Arm1_ABCD-rsfMRI_**************.tgz
```

-   Finally, download through the list remain.txt, e.g.
    `downloadcmd -t remain.txt -d image_files/`