
# Non-event audio
From data distribution
From other sources

# Learning from weakly labeled data
https://en.wikipedia.org/wiki/Weak_supervision

## Clip contains events/not

Postive: Clip contains one or more events
Negative: Clip contains 0 events
Standard formulation

## Clip has number of events

Number of events as label
For 1 minute clips == BPM
Is a much stronger label than presense / not?
Also much closer to the desired output from overall system

How to do "counting" in differentiable way?
Is just sum( 1.0 * (frames < threshold) )
Will be a bit noisy for events which straddle multiple frames
But if focusing only on onset, might not be much of an issue

Has this been reported in research yet?

## Clip has label proporsions

Learning from Label Proportions (LLP)

In Learning with label proportions (LLP)
the training data is provided in groups (or "bags"),
and only the proportion of each class in each group is known.
http://felixyu.org/pSVM.html

Hernández-González Jeronimo, Inza Iñaki, and Lozano Jose
A Learning bayesian network classifiers from label proportions.
Pattern Recognition, 46(12):3425–3440, 2013. [Google Scholar]

Proporsion can be derived from number of positive events,
since total number of frames in clips are known

Deep learning from label proportions with labeled samples
https://www.researchgate.net/publication/341210528_Deep_learning_from_label_proportions_with_labeled_samples
2020

End-to-end LLP solver based on convolutional neural networks (ConvNets),
called LLP with labeled samples (LLP-LS).
First, we reshape the cross entropy loss in ConvNets, so that it can combine the proportional information and labeled samples in each bag. Second, in order to comply with the training data in a bag manner, ADAM based on batch is employed to train LLP-LS.

Two-stage Training for Learning from Label Proportions
https://www.researchgate.net/publication/351841629_Two-stage_Training_for_Learning_from_Label_Proportions
https://arxiv.org/abs/2105.10635v1
2021

Existing deep learning based LLP methods utilize end-to-end pipelines
to obtain the proportional loss with Kullback-Leibler divergence between the bag-level prior and posterior class distributions.
In this paper, we regard these problems as noisy pseudo labeling, and instead impose the strict proportion consistency on the classifier with a constrained optimization as a continuous training stage for existing LLP classifiers. In addition, we introduce the mixup strategy and symmetric crossentropy to further reduce the label noise. Our framework is model-agnostic, and demonstrates compelling performance improvement in extensive experiments, when incorporated into other deep LLP models as a post-hoc phase. 

Learning from Label Proportions with Consistency Regularization
http://proceedings.mlr.press/v129/tsai20a/tsai20a.pdf
2020

Deep multi-class learning from label proportions
https://arxiv.org/abs/1905.12909v1
2019

Several approaches have been proposed with label proporsions
with linear models in the multiclass setting,
or with nonlinear models in the binary classification setting.
Here we investigate the more general nonlinear multiclass setting
compare two differentiable loss functions to train end-to-end deep neural networks from bags with label proportions.

## Weak-supervision Time-series Analysis
https://ir.library.oregonstate.edu/concern/graduate_thesis_or_dissertations/qr46r5921
2019

To reduce the labor-intensive annotation efforts associated with labeling a signal at a time-instance level,
coarse interval-level labeling is often considered.
We propose a framework that can efficiently model and analyze large-scale multi-channel time-series data and provide fine-grain label predictions from coarse interval-labeled data.
Since our focus is on time-series data with time-invariant events, we consider a convolutive modeling.
To extract time-invariant recurring patterns in time-series, we first propose a convolutive generative framework and use the resulting features for classification.
To learn a time-instance label model in a weak-supervision setting efficiently, we propose novel dynamic programming approaches (using both a chain and a tree structure).
Moreover, we extend the proposed weakly-supervised dictionary learning model for adapting both multiple clusters and multiple-scales.
As future work, we present an application of the proposed approach to deep learning.

## Learning Time Series Detection Models from Temporally Imprecise Labels
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6241530/
2017

Consider the problem of learning time series detection models from temporally imprecise labels.
The data consist of a set of input time series,
and supervision is provided by a sequence of noisy time stamps corresponding to the occurrence of positive class events.
Such temporally  imprecise labels occur in areas like mobile health research when human annotators are tasked with labeling the occurrence of very short duration events.
We propose a general learning framework for this problem that can accommodate different base classifiers and noise models.
We present results on real mobile health data showing that the proposed framework significantly outperforms a number of alternatives including:
- assuming that the label time stamps are noise-free
- transforming the problem into the multiple instance learning framework
- and learning on labels that were manually aligned

Primary assumption is that each observed positive event time stamp is generated probabilistically from a distribution centered close in time to a true positive instance.
We subsequently relax this assumption to allow for both false positive event time stamps and missed event time stamps.

! interesting to outperform manually aligned, and Multiple Instance Learning
retains temporal information 


# Deploying in production setting
Easiest way to get into peoples hands would be a web-app,
that can be ran on a mobile phone

- Find someone doing some beer brewing, with airlock
- Setup a Soundsensing device there
- Use Soundsensing compatible spectrogram for model
- Fetch spectrograms from Soundsensing API
