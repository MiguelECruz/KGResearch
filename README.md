# Effects of knowledge graph structural properties on their predictive performance

#### **Main programmer**: Miguel E. Cruz Molina | miguel.cruz15@upr.edu
#### **Research mentor**: Dr. Rafael A. Arce Nazario | rafael.arce@upr.edu

## Abstract

As recording and organizing relational data becomes a fundamental necessity in computational applications across multiple industrial domains, knowledge graphs (KGs) have become a popular option for modeling relationships between entities, in no small part due to their structural intuitiveness and general applicability. Recent appraisals of this potential have led to the sustained development of machine learning (ML) tools for embedding and extrapolating on existing KG datasets, with the purpose of aiding in statistical relational learning (SRL) tasks such as link prediction and entity classification. Although much literature exists on modifying and contrasting individual tools to identify ways in which their already plateauing efficiency can increase, literature analyzing the effects of preexisting graph characteristics on ML performance remains sparse. Through our research, we aim to prove that changes across these characteristics, particularly edge uniformity in relations guided by the Zipfian distribution, do reflect into corresponding changes in said model performance. Our results point towards differences in the studied parameter accounting for an increase in model accuracy across three distinct KG embedding predictive algorithms.

## Methodology

The present repository contains the results of our research, conducted from 2021-2022, on the effects of KG structural properties, particularly edge uniformity as dictated in relationships following the Zipfian distribution, on the performance of three KGE predictive algorithms. For this purpose, we developed an experiment tracking the performance of **240 machine learning models** synthetized through one of **three distinct KGE algorithms**, each one trained and tested over a different knowledge graph than the models produced under its same algorithm. Each graph was itself generated according to one out of **eight different graph configurations** (each of which was used to produce 10 knowledge graphs, for a total of **80 KGs**), with the only difference between configurations stemming from the *s* parameter used in relationship types following the Zipf distribution. The accuracy of the resulting models was then measured using **mean rank**, **mean reciprocal rank**, **hits@1**, **hits@10** and **hits@100** metrics, and **29 linear plots and boxplots** were generated and saved to analyze the effect of the original parameter variations.

To generate all original graphs, the [gMark](https://github.com/gbagan/gmark) program developed by Bagan et al. (2015) was used. gMark is an open-sourced C++ “practical framework that \[…\] takes a schema-driven approach” (Bagan et al., 2015) by generating both specific graph instances and query workloads in four different semantics for testing graph database systems. For the purposes of our research, only the first of these functionalities was employed during our experiment. Eight different configuration files were written, each one establishing a slightly distinct schema for a graph’s configuration, consisting of 5 types of entities and 4 types of relationships, three of them following Zipfian distributions (out of eight total ingoing and outgoing relationship distributions). The Zipfian parameter *s* remains equal among all three of these distributions but increases by a step of 0.5 from each schema to the next, with the values in all eight ranging from 0.5 to 4.0. All original configuration files contain commands for producing 10 graphs matching the specified schema, which, when processed through gMark, result in **80 textual files containing at least 30000 triples** each. Graph sizes are automatically adjusted to reflect entity and relationship proportions and distribution constraints. All graph files are then converted to comma-separated values (CSV) format before model synthesis.

Three KGE predictive algorithms were used to synthesize models (one each algorithm) over all 80 graphs. Following the example established by Costabello et al. (2020) in their [own lecture and tutorial](https://kge-tutorial-ecai2020.github.io/) regarding knowledge graph embeddings, we applied these models by using functions directly from [AmpliGraph](https://github.com/Accenture/AmpliGraph) (Costabello et al., 2019), an open-sourced Python library focused on machine learning application over KGs. The three algorithms chosen for this task were **TransE**, a translation-based model, and **DistMult** and **ComplEx**, both factorization-based models (Costabello et al., 2020). The triples of each graph were divided into training, validation and evaluation subsets, with the validation and evaluation subgraphs numbering **500** and **1000** triples each and all remaining triples falling in the training category. Three models were trained and tested for each division following the chosen algorithms, and the resulting metrics for each one were subsequently displayed and recorded. With the results obtained from the model synthesis part of this experiment, **23 additional DataFrames** were constructed, indicating the punctual metrics for each graph, schema and model, and their mean and standard deviation by configuration. Finally, **29 distinct plots** were generated for visualizing these results. 

All the code programmed for this experiment was written in Python and Git and can be read and replicated through the **Jupyter notebook** "Effects of knowledge graph structural properties on their predictive performance" included in static form in this repository, and through the following [link](https://colab.research.google.com/drive/19ExEC9jP56yx5Snj8qM5PJpw2Sn_JMX1#scrollTo=umsighIxtV9E) in an interactive Google Colab environment.

## Contents

The contents of this repository include the following 6 subdirectories, each one dedicated to a different step of the experiment described above:

1. `configs`: the 8 original configuration files written in XML to guide graph synthesis
2. `graphs`: files of the 80 knowledge graphs (10 by configuration) produced by gMark, in TXT and CSV formats
3. `models`: 240 models generated from the graph files (3 of each), divided by KG embedding algorithm 
4. `metrics`: 27 tabular files (9 by KGE algorithm) with metric results for each configuration and algorithm
5. `dataframes`: 23 tabular files with specific results for each metric 
6. `plots`: 8 linear graphs, 15 boxplots and 6 bar graphs displaying the results in `dataframes`

Additionally, we include a set of static files containing the Jupyter notebook used to produce and replicate our experiment, "Effects of knowledge graph structural properties on their predictive performance", with documentation in Spanish ~~and English~~. Mutable online versions of these files can be accessed for didactic purposes through [this link](https://colab.research.google.com/drive/19ExEC9jP56yx5Snj8qM5PJpw2Sn_JMX1#scrollTo=umsighIxtV9E) (ESP) and ~~this link (ENG)~~.

## References

*   Nickel, M. et al. (2015). A review of relational machine learning for knowledge graphs (pp. 11-33). In *Proceedings of the IEEE 104.1 2015*. DOI: 10.1109/JPROC.2015.2483592. Available [here](https://ieeexplore.ieee.org/document/7358050).

*   Bagan, G. et al. (2015). gMark: Schema-driven generation of graphs and queries. In *IEEE: Transactions on Knowledge and Data Engineering 2017*.

    *   [Original paper](https://arxiv.org/abs/1511.08386) describing the framework
    *   [GitHub repository](https://github.com/gbagan/gmark) with gMark files

*   Costabello, L. et al. (2020). Knowledge Graph Embeddings Tutorial: From theory to practice. In *European Congress on Artificial Intelligence 2020*.
    *   [Jupyter notebook](https://colab.research.google.com/drive/1Fcf8vkuaO6VCOB3MAZlpDebCAgyUnMBj?usp=sharing#scrollTo=17mJcCLovIkx) with tutorial of KGE model application
    *   [Website](https://kge-tutorial-ecai2020.github.io/) with outline, links and record of lecture 
    *   [Slideshow](https://kge-tutorial-ecai2020.github.io/ECAI-20_KGE_tutorial.pdf) provided in the lecture
    *   [Video](https://www.youtube.com/watch?v=gX_KHaU8ChI) of lecture

*   Costabello, L. et al. (2019). AmpliGraph
    *   [GitHub repository](https://github.com/Accenture/AmpliGraph) of library
    *   [Public documentation](https://docs.ampligraph.org/en/1.4.0/) of library


