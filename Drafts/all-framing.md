Brain-computer interface (BCI) systems establish a direct communcative link between the brain and an electronic system. \ref{wolpow2002} While the earliest systmes required [[[ electrodes implanted in the user's s ]]], newer work has used non-invasive electroencephelographs (EEG) to build proof-of-concept BCI systems ranging from brain-controlled keyboards [hex-o-spell] and wheelchairs [millan] to prosthetic arms and hands [tobi]. 

There are a few reasons why these systems have not been widely deployed outside of lab settings. For one, they require large, complex scanning caps, which are impractical for disabled users and generally undesirable for ergonomic reasons. Meanwhile, the data these caps produce is large, which could be computationally unwieldy on the mobile computing environments in which these systems will most likely be deployed (e.g., cellphones, embedded hardware, etc).

For BCI systems to reach wider adoption, they must acheive the same bitrates with fewer, and more comfortable sensors. Since naturalistic environments will also introduce interference in the signal, they must also cope with lower signal quality compared to their lab-based counterparts. How can we more effectively extract signal from EEG electrodes? 

In this study, we use recordings from a single, dry electroencephalographic (EEG) sensor to interrogate the efficacy of a signal quantization technique based on the logarithmic binning of power spectra over time. We model how our technique impacts the accuracy of the BCI's classifier and how it impacts the classifier's computational performance, especially at the short recording lengths necessary for quick, real-time interaction with computer systems. 

{{{{{not sure about this: By modelling how these factors scale relative to one another, we hope to work toward a theoretical framework for optimizing classification accuracy, computational expense and information transfer rate (ITR) in "in the wild" BCI systems.}}}}}}

# "In the wild" brain-computer interface

The wide adoption of BCI relies on two major streams of research: (i) the development of ergonomic sensors suitable for use in naturalitic settings and (ii) the ability to adapt lab-developed BCI strategies to the new constraints imposed by that these sensors. {........steal line on consumer EEG devices.........} Compared to their lab-based counerparts, ]these devices have many fewer electrodes, thus limited spatial resolution, and produce significantly noisier signals, as they do not require the application of conductive gels or the precise placement of sensors.

Past work has built several proof-of-concept BCIs with consumer-grade devices. impressive emotiv studies.....intro neurosky, several studies.

BCIs built with consumer-grade hardware still have relatively low ITR compared to those with full scanning caps (a maximum bits/sec was acheived by []). {{butttt.................did any of them really try calibratino/co-adaptive strategy?}}


# co-adaptive BCI

Blankertz et al (---) frame BCI learning as a cooperation between two adaptive systems: the brain and the BCI's software. By building systems in which the user and the BCI "co-adapt" during an interactive calibration phase, past work has turned BCI "novices" into users with decent control over the system in hours instead of days or weeks, and without the intervention of a researcher. \ref{} 

this ==> a calibration phase in which machine learning algorithms andtrained, re-trained on exemplar data as user gives feedback. this requires online processing of signals, even though the operation can be much more expensive than experienced in real-life environments (as different signal processing strategies are being compared). particularly important because users may need to calibrate BCI rather frequently, at least during the technology's infancy, so we need to be able to do it quickly.


# statistical signal processing in EEG-based BCI

Most commonly, BCI systems aim to recognize a user's mental cues as symbols so that they can be executed by a machine - a task that can be conceptualized as a pattern recognition problem \ref{lotte?whoever she cites?}. Its difficulty stems from the personal, non-stationary nature of mental representations. The "symbols" we wish to classify are different from person-to-person, and even change person-to-person over time \ref{}. .............................In order to compensate for variability in the signal, recent work has leveraged adaptive, machine learning approaches for classifying brainscan data.

{...........steal lines about how LDA's are good etc............}

before data gets fed to ML algo it must be classified.........signal extraction techniques have been developed, CSP to understand which electrdoes are informative.......

on the order of single electrodes, the most basic form of processing is to perform a FFT and analyze the resulting power spectrum. the majority of BCI systems bandpass this frequency spectrum between {x Hz..x Hz}, as these are the frequencies presumed to be of cortical origin (as opposed to, for instance, the signals produced by muscle contraction, which are presumed by most studies to be irrelevant). 