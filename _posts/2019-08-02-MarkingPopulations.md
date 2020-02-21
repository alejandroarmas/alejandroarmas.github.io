---
layout: article
title: Marking populations of honey bees for generating multivariate time series
tags: research interning bees machine-learning
aside:
    toc: true
  
---

<p>
    <img src="/assets/images/MarkingPopulations/cover.jpeg" alt="Cover photo"/>
    <br>
    <em>Honey Bees on comb 
    <a href="http://www.talkingwithbees.com/beekeeping/honeybees/honeybee-photos">[“Courtesy Talking With Bees”]</a>
    </em>
</p>

>Here's a blogpost originally from my time interning in Puerto Rico, I know Medium has a paywall so I decided I was going to have this on my website instead. I hope you enjoy!

To fully capture and characterize the behavior of any population of honey bees, or bees in general, you need a formal approach with no inherent biases. Dr. Agosto-Rivera’s research into understanding Circadian Rhythms with bees has been highly suggestive of “shift work” in the past, but remained uncertain as data collection was through human observations with no formal framework [5]. Two types of eusocial bees, Lassioglassum malachurum (sweat bee) [4] and Apis mellifera gAHB (gentle africanized honey bee), have been observed to exhibit individuality within a genetically identical population in context to their locomotion. To contrast, Drosophila melangaster (common fruit fly) exhibits no variation. Understanding this variation could potentially answer questions such as knowing if individual bee variation could be beneficial to the colony, if relaxed selection could somehow be related to seasonality and if this behavior could be the basis of of a natural form of shift work. Below I will describe the new approach, which combines bee tagging and deep neural networks, to mitigating the problem of biased data collection for the populations of 9 hives in relation to the bee problem according to Dr. Agosto-Rivera.

<p>
    <img src="/assets/images/MarkingPopulations/bees.gif" alt="Cover photo" width="45%" height="50%"/>
    <img src="/assets/images/MarkingPopulations/bees2.gif" alt="Cover photo" width="45%" height="50%"/>
    <br>
    <em> Honey Bees before and after the tagging process. [Source “me”]</em>
</p>



Experiment begins with newborn bees, merely one day old, called brood. They are diploid workers, all genetically similar. The goal of this study is to amass a total population of nearly 1000 tagged bees per colony. They are obtained from a special section in the hive and placed into an incubator imitating the temperature within the hive as they await being marked. This is the most optimal time to begin bee tagging as according to post-doctorate researcher Mehmet Ali Döke, the brood exoskeleton is still soft such that a sting will not be felt, nor will the muscles be fully developed and wings hardened enough for flight. Additionally, the tagging will identify each individual within the population through time and observation. For tagging, RFID tags have been proposed, but as they are expensive so we opted for 2D bar codes instead. To tag each bee, you must carefully grab a brood by its wings toward its abdomen, so that its thorax is more pronounced (figure 1) to then grab their feet such that the individual bee cannot rotate. This is preferable to grabbing the abdomen itself, as a minimal amount of force will cause liquid will gush out, meaning the definite death of your bee. As you are grabbing the feet of the bee, you will then place a tiny amount of superglue on its thorax and orient a QR code on top so that it faces the head of the bee. You must be careful to not add too much glue in this process, because the bee olfactory system is advanced enough to distinguish the scent and the hive will subsequently reject the brood (the bee will be murdered). Throughout this entire process it is generally advised to wear a glove in the hand holding the bee feet, so that you do not get stung, since to get stung means the death of a bee.

<p>
    <img src="/assets/images/MarkingPopulations/bees3.gif" alt="Cover photo" width="45%" height="50%"/>
    <img src="/assets/images/MarkingPopulations/bees4.gif" alt="Cover photo" width="45%" height="50%"/>
    <br>
    <em> Figure 1: Showcase how the bee should be handled during the tagging process. [Source “me”]</em>
</p>



# Neural network bee detection

UPR-Río Piedras’ Master student Ivan Rodriguez is credited for the development of a deep learning model for bee fanning behavior, pose detection of head, thorax, abdomen, and antennas, which can distinguish between pollen bearing and non-pollen bearing bees [3]. Using his method, we will obtain “98% recall for part detection and 95% of correct part association” [2] for the tagged bees.

<p>
    <img src="/assets/images/MarkingPopulations/bees5.gif" alt="Cover photo"/>
    <br>
    <em>Sample bee detection, pose estimation, pollen detection. [Source “Ivan F. Rodríguez”]
    </em>
</p>


This tool will serve an integral portion for the collection of time series data as the deep learning model will provide behavioral data of bee fanning, pollen intake, and exit/entrance into hive for each of the uniquely tagged bees. This dataset will provide the basis for multivariate time series analysis to answer questions posed at the beginning of the article. My work in this project, beyond bee tagging, is to discover chronotypes by creating wavelet transformations of this time series to cluster bees into homogeneous groups based on their time features. Additional analysis into chronotypes could prove useful in quantifying colony performance based on their shift work.

--------


[1] Edward Latorre, Kelvin López, Ivan F. Rodríguez, Matías Rosner Ortiz, Rémi Mégret, Tugrul Giray, José L. Agosto, “Recognition of Fanning Bees from Video using Convolutional Neural Networks”, SIDIM 2019, Humacao, March 1–2 2019.

[2] Ivan F. Rodríguez, Rémi Mégret, Roian Egnor, Kristin Branson, José L. Agosto, Tugrul Giray, Edgar Acuña . “Multiple Insect and Animal Tracking in Video using Part Affinity Fields”, Visual observation and analysis of Vertebrate And Insect Behavior (VAIB), International Conference on Pattern Recognition (ICPR), Beijin, China, 20–24 August 2018.

[3] Ivan F. Rodriguez, Kristin Branson, Edgar Acuña, Rémi Mégret, José L. Agosto-Rivera, Tugrul Giray, “Automatic monitoring of the foraging behavior of tagged and untagged honey bees”, SIDIM 2019, Humacao, March 1–2 2019.

[4] L.M. Wyman and M.H. Richards. Colony social organization of Lasioglossum malachurum Kirby (Hymenoptera, Halictidae) in Southern Greece , insectes Sociaux 50(3):201–211 , July 2003.

[5] Manuel Antonio Giannoni-Guzmán, Tugrul Giray, José L. Agosto-Rivera, Emmanuel Rivera, “Direct behavioral observations uncover shift work on honey bee Apis mellifera” , Entomological Society of America Annual Meeting 2013, November 2013.

