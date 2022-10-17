# Multi-Omics Graph cOnvolutional NETworks (MOGONET)

Multi-Omics Graph cOnvolutional NETworks (MOGONET) is a novel integrative method for biomedical classification. It jotly explores omics-specific learning and cross-omics correlation learning for effective multi-omics data classification.

This approaches from different biomedical classification applications using **mRNA** expression data, **DNA** methylation data, and **micoRNA** expresision data. Furthermore, MOGONET can identify important biomarkser from different omics data types related to the investigated biomedical problems.



## Methods

MOGONET is a framework for classification tasks with multi-omics data. Its workflow can be summarized into three components:

Keywords: **Graph Convolutional Networks (GCN)**, **View Correlation Discovery Network(VCDN)**

 1. [Preprocessing](#preprocessing)
 2. [Omics-specific learning via GCNs](#gcn)
 3. [Multi-omics integration via VCDN](#vcdn)

MOGONET is an end-to-end model, where both omics-specific **GCNs** and **VCDN** are trained jointly.

### Preprocessing

Preprocessing and feature preselection were performed on each omics data type individually to remove:

 - Noise
 - Artifact
 - Redundant features that may deteriorate perfomance of classfication tasks.

First, for DNA methylation data, only probles corresponding to probes corresponding to probles in the Illumina Infinium HumanMethylation27 BeadChip were retained for better interpretability of the results.

Then further filtered out features with no **signal** (zero mean values) or low variances. Specifically, applied different **variance filtering thresholds** for different types of omics data (0.1 fo mRNA expression data and 0.001 for DNA methylation data) as different omics data types came with different ranges.

Since omics data could contain redundant features that might have negative effects on classifciation performance, we further preselected omics features through statistical tests:
 
 > For each classfication task, ANOVA F-value was calculated sequentially using the training data to evaluate whether a feature was **significantly** different across different classes.

 > False discovery rate (FDR) controlling procedures were applied for multiple test compensation.

However, selecting too few features might also result in only selecting **highly correlated** features, which could potentially restrain the models from taking advantage of **complementay information** from diverse features. To avoid this:

 - Determined number of preselected features for each additional rule:
   + First principal component of data after feature preselection should explain $<50\% $ of the varince


Finally, individually scaled each type of omics data to [0, 1] through linear transformations for training MOGONET.


### GCN

**Graph Convolutional Networks (GCN)**

For each omics data type, a weighted sample similarity network was constructed from omics features. Then a GCN was trained using both omics features and corresponding **similarity network** for omics-specific learning.

While existing GCN models mainly focus on semi-supervised learning by propagating lables from labeld data to unlabeled ones, the values of these methods in clinical applications could be limited as the laerned GCN model cannot be directly applied to predicting new samples, whose data might not be available during training process.

Hence, the application of GCN in this paper was mainly of supervised learning. Where goal is to capture **intrinsic** structure of data through graphs during network training.

The benefit of graph NN in a supervised settings is that is not only captures local intra-class information due to multi-modal phenomena with each calss, but also seeks more discriminative features by considering inter-class information.

#### Proof 

By viewing each **sample** as node in the sample similarity network, the goal of each GCN in MOGONET is to learn a function of features on graph:

$$\mathcal{G} = (\mathcal{V}, \mathcal{E})$$

To perform classification tasks by utilizing both features of each **node** and **relationships** between nodes characterized by the graph $\mathcal{G}$. Therefore, a GCN model takes the following two inputs:

- Feature matrix $\mathbf{X} \in \mathbb{R}^{n \times d}$, where $n$ is **number of nodes**, $d$ is **number of input features**.

- Description of graph structur, which is represented in the form of an **adjancency** matrix $\mathbf{A} \in \mathbb{R}^{n\times n}$.

Moreover, a GCN can be built by **stacking** multiple convolutional layers, where each layer is defined as the following:

$$ \mathbf{H}^{(l + 1)} = f(\mathbf{H}^{(l)}, \mathbf{A})
= \sigma(\mathbf{A}\mathbf{H^{(l)}}\mathbf{W}^{(l)})
$$

where $\mathbf{H}^{(l)}$ is the **input of the lth layer**, and $\mathbf{W}^{(l)}$ is the **weight matrix** of the lth layer.

And $\sigma(.)$ denotes a **non-linear activation** function.

</br>

### VCDN

A cross-omics discovery **tensor** was calculated using **initial class probability predictions** from all omics-specific learning. A VCDN was then trained with cross-omics discovery **tensor** to produce final predictions.

VCDN can effectively learn the intra-omics and cross-omics label correlations in the higher-level label space for better classification with multi-omicsdata.	


