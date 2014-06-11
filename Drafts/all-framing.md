Brain-computer interface (BCI) systems establish a direct communcative link between the brain and an electronic system. \ref{wolpow2002} While the earliest systmes required [[[ electrodes implanted in the user's s ]]], newer work has used non-invasive electroencephelographs (EEG) to build proof-of-concept BCI systems ranging from brain-controlled keyboards [hex-o-spell] and wheelchairs [millan] to prosthetic arms and hands [tobi]. 

There are a few reasons why these systems have not been widely deployed outside of lab settings. For one, they require large, complex scanning caps, which are impractical for disabled users and generally undesirable for ergonomic reasons. Meanwhile, the data these caps produce is large, which could be computationally unwieldy on the mobile computing environments in which these systems will most likely be deployed (e.g., cellphones, embedded hardware, etc).

For BCI systems to reach wider adoption, they must acheive the same bitrates with fewer, and more comfortable sensors. Since naturalistic environments will also introduce interference in the signal, they must also cope with lower signal quality compared to their lab-based counterparts. How can we more effectively extract signal from EEG electrodes? 

In this study, we use recordings from a single, dry electroencephalographic (EEG) sensor to interrogate the efficacy of a signal quantization technique based on the logarithmic binning of power spectra over time. We model how our technique impacts the accuracy of the BCI's classifier and how it impacts the classifier's computational performance, especially at the short recording  lengths necessary for quick, real-time interaction with computer systems. 

{{{{{not sure about this: By modelling how these factors scale relative to one another, we hope to work toward a theoretical framework for optimizing classification accuracy, computational expense and information transfer rate (ITR) in "in the wild" BCI systems.}}}}}}

# Statistical signal processing in EEG-based BCI

Most commonly, BCI systems aim to recognize a user's mental cues as one of a finite set of discrete symbols - a task that can be conceptualized as a pattern recognition problem \ref{lotte?whoever she cites?}. The difficulty of this stems primarily from the non-stationary nature of mental cues. The "symbols" we wish to classify are expressed differently from person-to-person, and change even within the same person over time. \ref{}. 

In order to compensate for variability in the signal, recent work has leveraged adaptive classification algorithms to classify signals given labeled example data. {...........steal lines intro-ing classification algos..............steal lines about how LDA's are good etc............}



# Online co-adaptation 

Blankertz et al (---) frame BCI learning as a cooperation between two adaptive systems: the user's brain and the BCI's software algorithms. By building interfaces in which the user and the BCI "co-adapt" during an interactive calibration step, past work has turned BCI "novices" into competent users over the course of hours instead of days or weeks, and without manual calibration by a researcher. \ref{} 

Past work on co-adaptive BCI has employed a strategy in which preprocessed data are fed into a an adaptive classifier, which is optimized and recalculated either during intermittant, offline steps \ref{blankertz1,blankertz2} or continuously online \ref{vidaurre2006}. During calibration, users perform "labeled" (that is, known) mental gestures in order to produce samples for the classifier. Depending on the system, users may recieve real-time feedback on their performance. After several calibration steps, the system is able to estimate the user's control by assessing its classification accuracy on samples it has already recorded.

From a technical standpoint, this calibration phase amounts to the training and re-training of one or several adaptive algorithms (especially when several parameters are being simulatenously tested). This requires a great deal of signal processing to occur online, which entails not only the time required to train the classifier, but also the space required to handle the data and the time required to read and write the data from memory or from disk.

The computational expense involved with co-adaptive calibration is especially crucial, as most preliminary studies indicate that regular calibration and re-calibration will be a necessary component of BCI systems well into the foreseeable future due to the nonstationary nature of neural signals.


# Brain-computer interface "in the wild"

The wide adoption of BCI relies on two major streams of research: (i) the development of ergonomic sensors suitable for use in naturalitic settings and (ii) the ability to adapt lab-developed BCI strategies to the new constraints imposed by that these sensors. {........steal line on intro-ing consumer EEG devices.........} Compared to their lab-based counerparts, ]these devices have many fewer electrodes, thus limited spatial resolution, and produce significantly noisier signals, as they do not use gels to conduct signal nor do they assume that electrodes are precisely placed on the scalp.

Past studies have demonstrated the feasability several BCI systems with consumer-grade devices. {{{{{{{{{impressive emotiv studies.....intro neurosky, several studies.}}}}}}}}} However, BCIs built with consumer-grade hardware still have relatively low ITR compared to those with full scanning caps (a maximum bits/sec was acheived by []). However, most of these BCIs were aimed at applications other than the direct, real-time control of software interfaces (e.g., affect detection, cognitive load measurement, authentication). Studies aimed at implementing direct control interfaces with consumer hardware have mostly tried to replicate the methods of systems that employed large scanning caps \ref{??? lets get 2 here?}.

For effective BCI in naturalistic environments, we must squeeze more signal otu of our limited, and less reliable, sensors. Furthermore, we must be mindful of computational resources, partiuclarly during online calibration.


# Preprocessing EEG data in naturalistic settings

Before EEG data reaches the classifier, BCI systems employ a pre-processing step, the goal of which is to extract as much signal as possible from the EEG data, lest the classifiers lose generalizability due to excessive noise. Frequently-used extraction techniques involve CSP \ref{}, {{{ etc...... }}} On the order of single electrodes, however, the most basic pre-processing technique is the use of a fast fourier transform (FFT) to derive a power spectrum for each EEG reading in a time series. The majority of BCI systems bandpass this frequency spectrum between {x Hz..y Hz}, or simply lowpass the spectrum below {y Hz}, as these frequencies are presumed to be of cortical origin (as opposed to, for example, the signals produced by muscular activity, which are presumed by most studies to be irrelevant to the control of BCI systems). 





## methods


# SVM
 
Like LDAs, SVMs use a hyperplane to discriminate between classes; however, SVMs select the hyperplane that maximizes distance from the nearest training points, which has been shown to increase the SVM's generalizability \ref{lotte + C. J. C. Burges. A tutorial on supp ort v ector mac hines for pattern recognition. Know le dge Disc overy and Data Mining , 2, 1998 } 

Linear SVMs applied to BCI:

D. Garrett, D. A. P eterson, C. W. Anderson, and M. H. Thaut. Comparison of linear, nonlinear, and feature selection methods for eeg signal classiffcation. IEEE T r ansactions on Neural System and Rehabilitation Engine ering , 11:141{144, 2003.

A. Rak otomamonjy , V. Guigue, G. Mallet, and V. Alv arado. Ensemble of svms for impro ving brain computer in terface p300 sp eller p erformances. In International Confer enc e on A rticial Neur al Networks , 2005.