Brain-computer interface (BCI) systems establish a direct communcative link between the brain and an electronic system. \ref{wolpow2002} While early systmes required [[[ electrodes implanted in the user's s ]]], newer work has used non-invasive electroencephelographs (EEG) to build proof-of-concept BCI systems ranging from brain-controlled keyboards [hex-o-spell] and wheelchairs [millan] to prosthetic arms and hands [tobi]. 

There are a few reasons why these systems have not been widely deployed outside of lab settings. For one, they require large, complex scanning caps, which are impractical for disabled users and generally undesirable for ergonomic reasons. Meanwhile, the data these caps produce is large, which could be computationally unwieldy on the mobile computing environments in which these systems will most likely be deployed (eg., smartphones, watches, embedded systems in scanning devices, etc).

For BCI systems to find adoption "in the wild," they must acheive the acceptable bitrates with fewer and more comfortable sensors. They must calibrate to individual users quickly, and must run on mobile & wearable computing architectures. Since naturalistic environments will also introduce interference in the signal, they must also cope with lower signal quality than their lab-based counterparts. 

Can a small number of inexpensive, low-quality sensors acheive acceptable accuracy after a brief, online calibration phase? In this study, we use recordings from a single, dry electroencephalographic (EEG) sensor to interrogate the efficacy of a novel signal extraction technique based on the logarithmic binning of power spectra over time.

To wit, we find...............................................................................................................................................................................................................................................

## Brain-computer interface "in the wild"

The wide adoption of BCI relies on two major streams of research: (i) the development of ergonomic sensors suitable for use in naturalitic settings and (ii) the ability to adapt lab-developed BCI strategies to the new constraints imposed by that these sensors. {........steal line on intro-ing consumer EEG devices.........}  Compared to their lab-based counerparts, ]these devices have many fewer electrodes, thus limited spatial resolution, and produce significantly noisier signals, as they do not use gels to conduct signal nor do they assume that electrodes are precisely placed on the scalp.

Past work has demonstrated several mobile-ready BCI systems that use consumer-grade scanning devices. The Neurosky MindSet headset used in this study, employs a single, dry EEG electrode placed roughly at FP2, connects wirelessly to phones and computers, and sells for roughly 100USD. This headset has been used for cognitive load measurement, ERP detection and brain-based biometric authentication. \ref{lalalalalala} However, use of consumer EEGs for direct, real-time control of interfaces has been more tepid [swede who implemented snake; tepid wheelchair study]. 

To transition direct BCI into naturalistic environments, we must squeeze more signal out of fewer, and less reliable, sensors. One sensor is a good start. We must also be mindful of the computing architectures on which these systems will most likely be deployed: since BCIs are envisioned largely as always-available input devices, they will require mobile processors and perhaps even embedded processing systems; our computational resources may be more similar to that of a smartphone than of a desktop workstation, and it is feasible that we may need to do some processing "in the cloud" (ie., on a more powerful server to which the client sends data over the network, similar to the way Apple's Siri processes voice data). 


# Statistical signal processing in EEG-based BCI

For the control of interface systems, it is crucial that mental gestures be actuated intentionally, and that the system's interpretation be immediately verifiable by the user. \ref{some bci thing, "neurohype"}. Toward this end, BCI systems generally aim to recognize a user's mental gestures as one of a finite set of discrete symbols, which can be thought of as a pattern recognition task \ref{lotte?whoever she cites?}. The difficulty of this task stems primarily from the variable and non-stationary nature of neural signals: the "symbols" we wish to identify are expressed differently between individuals, and even vary within individuals from trial to trial. \ref{}.

In order to compensate for variability in BCI signals, recent work has leveraged adaptive classification algorithms to distinguish between mental gestures. {.........................steal lines intro-ing classification algos...................} {.................line explaining what a classifier is in terms of EEG and how we train one.......introduce the term "model" and how it applies here/why that term is relevant......................}


## Online co-adaptation 

Blankertz et al (---) frame BCI learning as a cooperation between two adaptive systems: the user's brain and the BCI's software algorithms. By building interfaces in which the user and the BCI "co-adapt" during an interactive calibration step, past work has turned BCI "novices" into competent users over the course of hours instead of days or weeks, and without manual calibration by a researcher. \ref{} 

Past work on co-adaptive BCI has used a several-step approach in which the system feeds preprocessed data to an adaptive classifier, which uses new and past data to optimize and recalculate itself, either during intermittant, offline steps \ref{blankertz1,blankertz2} or continuously online \ref{vidaurre2006}. During calibration, users perform "labeled" (that is, known) mental gestures in order to produce samples for the classifier. Meanwhile, the classifier performs various experiments in which it attempts to establish which features of the data are most informative. Systems may generate multiple models in parallel and combine their decisions democratically (an "ensemble approach"). After several calibration steps, the system is able to estimate the user's control by assessing its model's accuracy on samples it has already recorded.

From a technical standpoint, this calibration phase amounts to the training and re-training of one or several adaptive algorithms. Calibration can be processing-intensive work, especially when the system is computing multiple candidate models. This requires a great deal of online signal processing, which entails not only the computational time required to train the classifier, but also the space required to handle the data and the time required to read and write the data from memory or from disk.  as most preliminary studies indicate that regular calibration and re-calibration will be a necessary component of BCI systems well into the foreseeable future due to the nonstationary nature of neural signals.


## Co-adaptive BCI in naturalistic settings

this is where i dream a little..........just a little..........calibration and re-calibration is a part of the game.............happens whenever and is quick/well-supported........we can beam small amounst of data to a server, or do inexpensive processing on board if we are fast enough..............its the only way fwd..................................................









# Methods

Our research involved human subjects, and our experimental procedures were approved by an Institutional Review Board. We recruited 15 subjects to participate in our study, all of whom were UC Berkeley undergraduate or graduate students, Each subject met with investigators in a quiet, closed room for two 40-50 minute sessions on two separate days. We briefed subjects on the objective of the study, fitted them with a Neurosky MindSet heatset, and provided instructions for completing each task. As the subjects performed each task, we recorded readings from the headset.

## Tasks

...............steal from passthoughts latex.................

## Data Analysis

### Signal extraction

Before analyzing the data, we compute the power spectrum data using a fast fourier transform. We then compress the data in the temporal dimension, taking the middle \ital{n} seconds of the recording, where \ital{n} is {0.5, 1, 2, 3, 4, 5, 6, 7, 8, 9}. 

Second, we {..............logarithmic binning....................}

Finally, we create a one-dimensional signal by flattening each bin in the time dimension, computing the mean magnitude of each bin over all readings in the recording. The resulting signal is a one-dimensional row vector with one entry for each each measured frequncy bin.


{{{{{{{{{{{should we say something about how we dont bandpass????
The majority of BCI systems bandpass this frequency spectrum between {x Hz..y Hz}, or simply lowpass the spectrum below {y Hz}, as these frequencies are presumed to be of cortical origin (as opposed to, for example, the signals produced by muscular activity, which are presumed by most studies to be irrelevant to the control of BCI systems). However, recent work has shown that there is meaningful signal outside the canonical 1-30Hz range \ref{garripelli milan 2013}, so we include it in our analysis.}}}}}}

### Classification

Support vector machines (SVM) are a set of supervised machine learning methods that take labeled example data to create a model that can be used to predict the classes of unlabeled data. SVMs use a hyperplane (an n-dimensional construct in n+1 dimensional space) to draw discriminatory boundaries between classes. In contrast to linear discriminant analysis, which has a long history of use in BCIs, SVMs select the hyperplane that maximizes distance from the nearest training points, which has been shown to increase the model's generalizability \ref{lotte + C. J. C. Burges. A tutorial on supp ort v ector mac hines for pattern recognition. Know le dge Disc overy and Data Mining , 2, 1998 } For SVM's applied to BCI: {D. Garrett, D. A. P eterson, C. W. Anderson, and M. H. Thaut. Comparison of linear, nonlinear, and feature selection methods for eeg signal classiffcation. IEEE T r ansactions on Neural System and Rehabilitation Engine ering , 11:141{144, 2003. A. Rak otomamonjy , V. Guigue, G. Mallet, and V. Alv arado. Ensemble of svms for impro ving brain computer in terface p300 sp eller p erformances. In International Confer enc e on A rticial Neur al Networks , 2005.}

In this study, we use LinearSVC, a wrapper for Liblinear written in Python. \ref{liblinear,sk-learn} We chose LinearSVC primarily because its underlying C implementation is fast, and because linear kernels performed as well or better than nonlinear ones, corroborating the findings of previous studies. \ref{} We use the default settings for LinearSVC - a C of 1.0, squared hinge loss function, and a tolerance parameter of of 1e-4.


## Per-user calibration

We conducted a calibration step for each participant. .........................explain the calibration task...................... We repeated this process at various recording lengths and at various bin sizes (enumerated in \fig{}).

to simulate IRL we found the best-performing task-pair, but we also found the accuracy for every task pair we tried, which btw was all possible pairs of 2 tasks.




# Results