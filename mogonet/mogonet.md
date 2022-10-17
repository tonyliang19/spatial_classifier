# Multi-Omics Graph cOnvolutional NETworks (MOGONET)

Multi-Omics Graph cOnvolutional NETworks (MOGONET) is a novel integrative method for biomedical classification. It jotly explores omics-specific learning and cross-omics correlation learning for effective multi-omics data classification.

This approaches from different biomedical classification applications using **mRNA** expression data, **DNA** methylation data, and **micoRNA** expresision data. Furthermore, MOGONET can identify important biomarkser from different omics data types related to the investigated biomedical problems.



## Methods

MOGONET is a framework for classification tasks with multi-omics data. Its workflow can be summarized into three components:

Keywords: **Graph Convolutional Networks (GCN)**, **View Correlation Discovery Network(VCDN)**

 1. [Preprocessing](# Preprocessing)
 2. [Omics-specific learning via GCNs](# GCN)
 3. [Multi-omics integration via VCDN](# VCDN)

MOGONET is an end-to-end model, where both omics-specific **GCNs** and **VCDN** are trained jointly.

### Preprocessing

Preprocessing and feature preselection were performed on each omics data type individually to remove:
 - Noise
 - Artifact
 - Redundant features that may deteriorate perfomance of classfication tasks.



### GCN

**Graph Convolutional Networks (GCN)**

For each omics data type, a weighted sample similarity network was constructed from omics features. Then a GCN was trained using both omics features and corresponding **similarity network** for omics-specific learning.

### VCDN

A cross-omics discovery **tensor** was calculated using **initial class probability predictions** from all omics-specific learning. A VCDN was then trained with cross-omics discovery **tensor** to produce final predictions.

VCDN can effectively learn the intra-omics and cross-omics label correlations in the higher-level label space for better classification with multi-omicsdata.	
