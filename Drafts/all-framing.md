

## Online co-adaptation 

Coming to control a BCI system requires more than adaptive algorithms. Blankertz et al (---) frame BCI learning as a cooperation between two adaptive systems: the BCI's algorithms and the human user. By building interfaces in which the user and the BCI "co-adapt" during an interactive calibration step, past work has turned BCI "novices" into competent users over the course of hours instead of days or weeks, and without manual calibration by a researcher. \ref{} 

Past work on co-adaptive BCI has used a several-step approach in which the system feeds preprocessed data to an adaptive classifier, which uses new and past data to optimize and recalculate itself, either during intermittant, offline steps \ref{blankertz1,blankertz2} or continuously online \ref{vidaurre2006}. During calibration, users perform "labeled" (that is, known) mental gestures in order to produce samples for the classifier. Meanwhile, the classifier performs various experiments in which it attempts to establish which features of the data are most informative. Systems may generate multiple models in parallel and combine their decisions democratically (an "ensemble approach"). After several calibration steps, the system is able to estimate the user's control by assessing its model's accuracy on samples it has already recorded.

From a technical standpoint, this calibration phase amounts to the training and re-training of one or several adaptive algorithms. Calibration can be processing-intensive work, especially when the system is computing multiple candidate models. This requires a great deal of online signal processing, which entails not only the computational time required to train the classifier, but also the space required to handle the data and the time required to read and write the data from memory or from disk.  as most preliminary studies indicate that regular calibration and re-calibration will be a necessary component of BCI systems well into the foreseeable future due to the nonstationary nature of neural signals.


## Co-adaptive BCI in naturalistic settings


For the control of interface systems, it is crucial that mental gestures be actuated intentionally, and that the system's interpretation be immediately verifiable by the user. 

this is where i dream a little..........just a little..........calibration and re-calibration is a part of the game.............happens whenever and is quick/well-supported........we can beam small amounst of data to a server, or do inexpensive processing on board if we are fast enough..............its the only way fwd..................................................









# Methods

Our research involved human subjects, and our experimental procedures were approved by an Institutional Review Board. We recruited 15 subjects to participate in our study, all of whom were UC Berkeley undergraduate or graduate students, Each subject met with investigators in a quiet, closed room for two 40-50 minute sessions on two separate days. We briefed subjects on the objective of the study, fitted them with a Neurosky MindSet heatset, and provided instructions for completing each task. As the subjects performed each task, we recorded readings from the headset.

## Tasks

...............steal from passthoughts.................

## Data Analysis

### Signal extraction

Before analyzing the data, we compute the power spectrum data using a fast fourier transform. We then compress the data in the temporal dimension, taking the middle \ital{n} seconds of the recording, where \ital{n} is {0.5, 1, 2, 3, 4, 5, 6, 7, 8, 9}. 

Second, we {..............logarithmic binning....................}

Finally, we create a one-dimensional signal by flattening each bin in the time dimension, computing the mean magnitude of each bin over all readings in the recording. The resulting signal is a one-dimensional row vector with one entry for each each measured frequncy bin.


{{{{{{{{{{{should we say something about how we dont bandpass????
The majority of BCI systems bandpass this frequency spectrum between {x Hz..y Hz}, or simply lowpass the spectrum below {y Hz}, as these frequencies are presumed to be of cortical origin (as opposed to, for example, the signals produced by muscular activity, which are presumed by most studies to be irrelevant to the control of BCI systems). However, recent work has shown that there is meaningful signal outside the canonical 1-30Hz range \ref{garripelli milan 2013}, so we include it in our analysis.}}}}}}

### Classification

Support vector machines (SVM) are a set of supervised machine learning methods that take labeled example data to create a model that can be used to predict the classes of unlabeled data. SVMs use a hyperplane (an n-dimensional construct in n+1 dimensional space) to draw discriminatory boundaries between classes. In contrast to linear discriminant analysis, which has a long history of use in BCIs, SVMs select the hyperplane that maximizes distance from the nearest training points, which has been shown to increase the model's generalizability \ref{lotte + C. J. C. Burges. A tutorial on supp ort v ector mac hines for pattern recognition. Know le dge Disc overy and Data Mining , 2, 1998 } For SVM's applied to BCI: {D. Garrett, D. A. P eterson, C. W. Anderson, and M. H. Thaut. Comparison of linear, nonlinear, and feature selection methods for eeg signal classiffcation. IEEE T r ansactions on Neural System and Rehabilitation Engine ering , 11:141{144, 2003. A. Rak otomamonjy , V. Guigue, G. Mallet, and V. Alv arado. Ensemble of svms for impro ving brain computer in terface p300 sp eller p erformances. In International Confer enc e on A rticial Neur al Networks , 2005.}

In this study, we use LinearSVC, a wrapper for Liblinear exposed in Python through the scikit learn library. \ref{liblinear,sk-learn} We chose LinearSVC primarily because its underlying C implementation is very performant, and because linear kernels performed as well or better than nonlinear ones in early experimentation, corroborating the findings of previous studies. \ref{} We use the default settings for LinearSVC - a C of 1.0, squared hinge loss function, and a tolerance parameter of of 1e-4.


## Per-user calibration

We conducted a simulated calibration step for each participant. For each subject, we generated every possible pair of two tasks and cross-validated our SVM seven times on that subject's recordings for those two tasks. We used sk-learn's built-in cross-validation toolkit, which was configured to perform each of the seven cross-validation steps using different splits of trial data in the training and testing sets. For every task pair processed, we recorded mean classification across all cross-validation trials. We repeated this calibration process for all users at every combination of recording length and bin size. 


% TODO: ALSO AT TESTING TIME!
As an additional performance audit, we timed our SVM at training time. In order to establish a proper estimate, took two randomly selected subjects and two randomly selected task pairs, then fit an SVM to all data in those task pairs, and repeated this process ten thousand times. We report the minimum time of all trials. We time the SVM after all data has been loaded to memory, ignoring the time it takes to load the data from disk.


# Results

## Classification 



{.........figure of best-case accuracy at different bin sizes and times............}


We take particular interest in the accuracy of each subject's best-case task pair, as we predict this task pair would acheive the best discrimatory power.  We acheived excellent best-case performance overall, and maintained an estimated {x%} accuracy among {all [but x]} subjects, even at recording lengths of 1/2 second.

Surprisingly, classification was better than chance even at a bin size of {x}, meaning that each feature vector in the training and testing sets contained only {x} features. {.........report a regression?.........}

{.............figure of classification accuracy v. bin size...............}

{.............report regression between classification accuracy and bin-size, length, subject, taskpair etc..............}


## Performance

{.....figure of performance v speed....}

{....report regression between performance and speed.....}

% TODO: A REGRESSION ON TEST TIME AS WELL!!!!!!!


# Discussion

We find that logarithmic binning dramatically decreases the computational expense of EEG-based calibration and classification without a signfiicant detriment to accuracy. 

Logarithmic binning could enable co-adaptive, online BCI with as few as one dry EEG sensor, making online calibration much more performant on mobile or embedded processors with limited computational resources. Alternatively, since logarithmic dramatically decreases the size of data fed to the classification algorithm, the technique could allow calibration to occur "in the cloud" - the BCI could pre-process the data on board, bin it, and ship this data to a more powerful server, which could process it online. By some combination of cloud-based and on-board processing, BCIs could gain from the accuracy of computationally expensive analytics without having to perform these computations on-board.


Future work:

- 






























