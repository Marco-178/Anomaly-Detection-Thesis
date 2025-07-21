## Anomaly Detection Thesis

This repo stores the code implementing anomaly detection techniques on a given dataset. This has been done as part of my Bachelor's thesis in 2024. Here is a relevant paper discussing the topic: [Deep Learning for Time Series Anomaly
Detection: A Survey](https://doi.org/10.48550/arXiv.2211.05244).

Table of Contents
=================

   * [Introduction](#introduction)
      * [What is anomaly detection](#what-is-anomaly-detection)
   * [Code](#code)
      * [Tools used](#tools-used)
      * [Usage](#usage)
   * [Discussion](#discussion)
      * [Other useful papers](#other-useful-resources)


# Introduction
The thesis is focused on studying the general problem of anomaly detection, implementing anomaly detection algorithms and applying them on real-world data provided by a private company. Then the results of the various algorithms employed are compared and discussed.

## What is anomaly detection
Given an industrial machine, it is possible to detect deviations in the collected data which could indicate machine degradation or imminent malfunction. The the goal of Anomaly Detection algorithms is to exactly learn when deviations happen and detect them in real-time. 

These techniques can be a useful tool for optimizing the resilience of industrial processes, for example, by enabling the prediction of necessary maintenance interventions for industrial systems. These techniques not only allow for the precise identification of such deviations, but also enable dynamic responses to the emergence of previously unseen anomalies.

The field has particularly expanded its application prospects in the domain of time series, where data can follow particularly complex patterns. 

# Code
The [time_series.ipynb](./time_series.ipynb) file provides the code used for the implementation on the first section and the results on different types of unbalanced datasets for the next sections.

## Tools used

__Programming Language:__ Python 3.13+

__Libraries used for implementing the algorithms:__ [Scikit-learn](https://github.com/scikit-learn/scikit-learn), [Tensorflow](https://github.com/tensorflow/tensorflow), [DeepOD](https://github.com/xuhongzuo/DeepOD), [kneed](https://github.com/arvkevi/kneed), [lof_autotuner](https://github.com/vsatyakumar/automatic-local-outlier-factor-tuning).

## Usage
The code provided in the [time_series.ipynb](./time_series.ipynb) file can be run on Colab, Anaconda or locally as a .py file:

```bash
python time_series.py <FILEPATH> <FILENAME> <FILENAME_TRAIN> <NUM_COMPONENTS>
```
Where:
| Parameter | Description |
|-----------|-------------|
| `<FILEPATH>` | Path to the directory containing the datasets |
| `<FILENAME>` | Name of the test file (retrieved as `<FILEPATH>/Noise/<FILENAME>.csv`) |
| `<FILENAME_TRAIN>` | Name of the training file (retrieved as `<FILEPATH>/Training e Test/<FILENAME_TRAIN>.csv`) |
| `<NUM_COMPONENTS>` | Number of features in the dataset |

### Example
```bash
python time_series.py ./data machine_test machine_train 10
```

### Dataset Structure

The datasets should be structured as follows:

**Required Format:**
- **First `NUM_COMPONENTS - 1` columns:** Feature data
- **Last column:** Ground truth labels (0 = normal, 1 = anomaly)

**Directory Structure:**
```
<FILEPATH>/
├── Noise/
│   └── <FILENAME>.csv          # Test dataset
└── Training and Test/
    └── <FILENAME_TRAIN>.csv    # Training dataset
```

**Example CSV Structure:**
```csv
feature_1,feature_2,feature_3,...,feature_n,label
1.2,0.5,2.1,...,0.8,0
0.9,1.3,1.7,...,1.2,1
...
```

The ground truth labels in both datasets are used to evaluate the performance metrics of the anomaly detection algorithms.

## Comments
Some comments are in Italian since the thesis is written for a Italian university.

# Discussion
The content of the thesis will be re-adapted in a dedicated blogpost as a educational contribution.

## Other useful resources
Here is a list of papers and other resources which have been studied before implementing the code. The papers span different topics such as curse of dimensionality and dimensionality reduction techniques (PCA, t-SNE, UMAP), ML and DL algorithms for anomaly detection.

### Curse of Dimensionality and Dimensionality Reduction

*    L.J.P. van der Maaten, E.O. Postma, and H.J. van den Herik. [Dimensionality Reduction: A Comparative Review](https://lvdmaaten.github.io/publications/papers/TR_Dimensionality_Reduction_Review_2009.pdf). Technical Report TiCC-TR 2009-005, Tilburg University, 2009.
*    Jonathon Shlens. [A Tutorial on Principal Component Analysis](http://arxiv.org/abs/1404.1100). Computing Research Repository (CoRR), abs/1404.1100, 2014.
*    Quan Wang. [Kernel Principal Component Analysis and its Applications in Face Recognition and Active Shape Models](https://arxiv.org/abs/1207.3538), 2014.
*    CMU Barnabàs Pòzcos. Manifold Learning.
*    Geoffrey E Hinton and Sam Roweis. [Stochastic Neighbor Embedding](https://proceedings.neurips.cc/paper_files/paper/2002/file/6150ccc6069bea6b5716254057a194ef-Paper.pdf). volume 15. MIT Press, 2002.
*    Martin Wattenberg, Fernea Viégas, and Ian Johnson. [How to Use t-SNE Effectively](https://doi.org/10.23915/distill.00002). Distill, 2016.
*    Laurens van der Maaten and Geoffrey Hinton. [Visualizing Data Using t-SNE](http://jmlr.org/papers/v9/vandermaaten08a.html). Journal of Machine Learning Research, 2008.
*    Leland McInnes. [How UMAP Works](https://umap-learn.readthedocs.io/en/latest/how_umap_works.html), 2018.
*    Leland McInnes, John Healy, and James Melville. [UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction](https://arxiv.org/abs/1802.03426). The Journal of Open Source Software (JOSS), 2020.
*    Andy Coenen and Adam Pearce. [Understanding UMAP](https://pair-code.github.io/understanding-umap/).
*    Dmitry Kobak and George Linderman. [Initialization is critical for preserving global data structure in both t-SNE and UMAP](https://doi.org/10.1038/s41587-020-00809-z). Nature Biotechnology, 2021.



### Machine Learning Algorithms for Anomaly Detection
*    Mark Schwabacher, Nikunj Oza, and Bryan Matthews. [Unsupervised Anomaly Detection for Liquid-Fueled Rocket Propulsion Health Monitoring](https://doi.org/10.2514/1.42783). Technical Report NASA/TP-2009-214228, NASA Ames Research, 2009.
*    Arthur Zimek, Erich Schubert, and Hans-Peter Kriegel. [A survey on unsupervised outlier detection in high-dimensional numerical data](https://doi.org/10.1002/sam.11161). Statistical Analysis and Data Mining: The ASA Data Science Journal, 2012.
*    M. Ester, H.-P. Kriegel, J. Sander, and X. Xu. [A Density-Based Algorithm for Discovering Clusters in Large Spatial Databases with Noise](https://www.aaai.org/Papers/KDD/1996/KDD96-037.pdf). AAAI Press, 1996.
*    Markus Breunig, Peer Kröger, Raymond Ng, and Joerg Sander. [LOF: Identifying Density-Based Local Outliers](https://doi.org/10.1145/342009.335388).
*    Stephen Howard. The Elliptical Envelope. 2007.
*    Fei Tony Liu, Kai Ting, and Zhi-Hua Zhou. [Isolation Forest](https://doi.org/10.1109/ICDM.2008.17).
*    David Tax and Robert Duin. [Support Vector Data Description](https://doi.org/10.1023/B:MACH.0000008084.60811.49).
  


### Deep Learning Algorithms for Anomaly Detection
*    Zahra et al. Zamanzadeh Darban. [Deep Learning for Time Series Anomaly Detection: A Survey](https://doi.org/10.48550/arXiv.2211.05244). Association For Computing Machinery, 2022.
*    Hongzuo Xu, Guansong Pang, Yijie Wang, and Yongjun Wang. [Deep isolation forest for anomaly detection](https://doi.org/10.1109/TKDE.2023.3270293). IEEE Transactions on Knowledge and Data Engineering, 2023.
*    Lukas et al. Ruff. [Deep One-Class Classification](https://proceedings.mlr.press/v80/ruff18a.html). In Jennifer Dy and Andreas Krause, editors, Proceedings of the 35th International Conference on Machine Learning, volume 80 of Proceedings of Machine Learning Research. PMLR, 2018.



### Others
*    Kevin P. Murphy. Machine Learning: A Probabilistic Perspective. The MIT Press, Cambridge, MA, 2012.
*    Giuliano Mazzanti and Valter Roselli. Appunti di Algebra lineare, Geometria analitica, Tensori. Pitagora, Bologna, 2013. (italian)
*    Yanzhao Jhu. [Deep Learning and Information Theory](https://jhui.github.io/2017/01/05/Deep-learning-Information-theory/), 2017.
*    Satya Kumar Vadlamani. [Automatic-Local-Outlier-Factor-Tuning](https://github.com/vsatyakumar/automatic-local-outlier-factor-tuning).
*    Zekun Xu, Deovrat Kakde, and Arin Chaudhuri. [Automatic Hyperparameter Tuning Method for Local Outlier Factor, with Applications to Anomaly Detection](https://doi.org/10.1109/bigdata47090.2019.9006151). IEEE, 2019.


