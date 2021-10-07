---
layout: default
title: Datasets
nav_order: 2
parent: Storage Guide
---
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

<span style="background-color:orange">\* Not preprocessed</span>

Collaborative spreadsheet:
<https://drive.google.com/file/d/126Su7fBqaVAjefCe4s4Prk9qk_zdzsVy/view?usp=sharing>

| Name                           | Location                                                                   | fMRI                                             | sMRI                                             | dMRI                                              | SNIP | Groups                           | Free to use?     | Contact                         |
|--------------------------------|----------------------------------------------------------------------------|--------------------------------------------------|--------------------------------------------------|---------------------------------------------------|------|----------------------------------|------------------|---------------------------------|
| BSNIP                          | /data/analysis/collaboration/NeuroMark/Data/BSNIP                          | 1354                                             | 1354                                             |                                                   | 628  | HC, SZ, BP, Relatives            | Yes              | zfu \[at\] gsu \[dot\] edu      |
| FBIRN                          | /data/analysis/collaboration/NeuroMark/Data/FBIRN                          | 368                                              | 368                                              |                                                   | 278  | HC, SZ                           | Yes              | zfu \[at\] gsu \[dot\] edu      |
| COBRE                          | /data/analysis/collaboration/NeuroMark/Data/COBRE                          | 204                                              | 204                                              |                                                   | 226  | HC, SZ, BP                       | Yes              | zfu \[at\] gsu \[dot\] edu      |
| Peter Kochunov (U of Maryland) | /data/analysis/collaboration/NeuroMark/Data/PK                             | 457                                              | 444                                              |                                                   | 1076 | HC, SZ                           | Yes              | zfu \[at\] gsu \[dot\] edu      |
| Chinese Schizophrenia dataset  | /data/analysis/collaboration/NeuroMark/Data/Unactivated_Data/ChineseSZ     | 1614                                             | 954                                              |                                                   |      | HC, SZ                           | Needs permission | jsui \[at\] gsu \[dot\] edu     |
| UCLA-CNP                       | /data/analysis/collaboration/NeuroMark/Data/Unactivated_Data/UCLA-CNP      | <span style="background-color:orange">261</span> | <span style="background-color:orange">261</span> | <span style="background-color:orange">261</span>  |      | HC, SZ                           | Yes              | zfu \[at\] gsu \[dot\] edu      |
| Schizophrenia Johns Hopkins    | /data/collaboration/NeuroMark/Data/SZ_JH                                   | 180                                              | 180                                              |                                                   |      | HC, SZ                           | Yes              | zfu \[at\] gsu \[dot\] edu      |
| HCP early psychosis            | /data/analysis/collaboration/NeuroMark/Data/HCP_EarlyP                     | 169                                              | 169                                              | <span style="background-color:orange">169</span>  |      | HC, early psychosis patients     | Yes              | zfu \[at\] gsu \[dot\] edu      |
| ABIDE1                         | /data/analysis/collaboration/NeuroMark/Data/Autism/ABIDE1                  | 1112                                             | 1112                                             |                                                   |      | HC, ASD                          | Yes              | zfu \[at\] gsu \[dot\] edu      |
| ABIDE2                         | /data/analysis/collaboration/NeuroMark/Data/Autism/ABIDE2                  | 1113                                             | 1113                                             | <span style="background-color:orange">318</span>  |      | HC, ASD (some longitudinal data) | Yes              | zfu \[at\] gsu \[dot\] edu      |
| OSUCH                          | /data/analysis/collaboration/NeuroMark/Data/OSUCH                          | 103                                              | 156                                              |                                                   |      | HC, mood disorder                | Yes              | zfu \[at\] gsu \[dot\] edu      |
| ECT (UCLA & UNM ECT data)      | /data/analysis/collaboration/NeuroMark/Data/Depression/ECT                 | 180                                              | 180                                              |                                                   |      | HC, MDD (before & after ECT)     | Yes              | zfu \[at\] gsu \[dot\] edu      |
| Chinese Major depression data  | /data/analysis/collaboration/NeuroMark/Data/Depression/MDD_China           | 600                                              | 590                                              |                                                   |      | HC, MDD                          | Needs permission | jsui \[at\] gsu \[dot\] edu     |
| ADNI                           | /data/analysis/collaboration/NeuroMark/Data/ADNI                           | 373                                              | 1625                                             | <span style="background-color:orange">383</span>  |      | HC, AD, MCI, EMCI, LMCI          | Yes              | zfu \[at\] gsu \[dot\] edu      |
| STANFORD-ADRC                  | /data/analysis/collaboration/NeuroMark/Data/Unactivated_Data/STANFORD-ADRC | <span style="background-color:orange">204</span> | <span style="background-color:orange">204</span> |                                                   |      | HC, AD, MCI, LBD, PD             | Yes              | zfu \[at\] gsu \[dot\] edu      |
| MarkVCID                       | /data/analysis/collaboration/NeuroMark/Data/MarkVCID                       | 97                                               | 20                                               | <span style="background-color:orange">5</span>    |      | HC, LA, AD, SIVD, Mixed dementia | Yes              | zfu \[at\] gsu \[dot\] edu      |
| OASIS Cross-Sectional          | /data/analysis/collaboration/NeuroMark/Data/OASIS/OASIS Cross-Sectional    |                                                  | <span style="background-color:orange">436</span> |                                                   |      | HC, AD                           | Yes              | zfu \[at\] gsu \[dot\] edu      |
| OASIS Longitudinal             | /data/analysis/collaboration/NeuroMark/Data/OASIS/OASIS Longitudinal       |                                                  | <span style="background-color:orange">373</span> |                                                   |      | HC, AD                           | Yes              | zfu \[at\] gsu \[dot\] edu      |
| OASIS3                         | /data/analysis/collaboration/NeuroMark/Data/OASIS/OASIS3                   | 1691                                             | 2217                                             | <span style="background-color:orange">1205</span> |      | HC, AD, MCI                      | Yes              | zfu \[at\] gsu \[dot\] edu      |
| ADHD200                        | /data/analysis/collaboration/NeuroMark/Data/ADHD/ADHD200                   | 949                                              | 949                                              |                                                   |      | HC, ADHD-C, ADHD-H/I, ADHD-I     | Yes              | zfu \[at\] gsu \[dot\] edu      |
| Suijing ADHD dataset           | /data/analysis/collaboration/NeuroMark/Data/ADHD/ADHD_Suijing              | 189                                              | 116                                              |                                                   |      | HC, ADHD                         | Needs permission | jsui \[at\] gsu \[dot\] edu     |
| ADHD unknown                   | /data/analysis/collaboration/NeuroMark/Data/ADHD/ADHD_unknown              | 197                                              | 197                                              |                                                   |      | HC, ADHD                         | No               | zfu \[at\] gsu \[dot\] edu      |
| Hutchison's substance use      | /data/analysis/collaboration/NeuroMark/Data/Addiction                      | 989                                              | 989                                              |                                                   |      | Alcohol, Nicotine disorder       | Needs permission | vvergara \[at\] gsu \[dot\] edu |
| Anees Neuroimage data          | /data/analysis/collaboration/NeuroMark/Data/Anees_NIMG                     |                                                  | 6008                                             |                                                   |      | HC and other diseases            | Yes              | aabrol \[at\] gsu \[dot\] edu   |
| GSP                            | /data/analysis/collaboration/NeuroMark/Data/GSP                            | 1182                                             | 1182                                             |                                                   |      | HC                               | Yes              | zfu \[at\] gsu \[dot\] edu      |
| HCP                            | /data/analysis/collaboration/NeuroMark/Data/HCP                            | 1115                                             | 1058                                             |                                                   |      | HC                               | Yes              | zfu \[at\] gsu \[dot\] edu      |
| ABCD                           | /data/collaboration/NeuroMark/Data/ABCD                                    | 11764 (before Release 2.0)                       | 11764                                            | <span style="background-color:orange">3976</span> |      | HC                               | Yes              | zfu \[at\] gsu \[dot\] edu      |
| UK-BIO Bank                    | /data/collaboration/NeuroMark/Data/UKBiobank                               | 39342                                            | 41182                                            |                                                   |      | HC and self-reported diagnosis   | Yes              | zfu \[at\] gsu \[dot\] edu      |
| Total                          | 65807                                                                      | 75405                                            | 6317                                             | 2563                                              |      |                                  |                  |                                 |

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