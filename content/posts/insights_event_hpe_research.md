+++
title = "Event-cameras, Human Pose Estimation, and what to take home"
author = ["Gianluca Scarpellini"]
lastmod = 2021-05-03T16:48:54+02:00
tags = ["event-cameras"]
draft = false
weight = 1003
noauthor = true
nocomment = true
nodate = true
nopaging = true
noread = true
+++

As I write, [my paper about event-cameras and human-pose estimation](https://iit-pavis.github.io/lifting%5Fevents%5Fto%5F3d%5Fhpe/) has been
accepted at the Computer Vision and Pattern Recognition workshop on
event-cameras[^fn:1]. If you do
not know what an event-camera is, I wrote about them [[[{{< relref "event-cameras" >}}]({{< relref "event-cameras" >}}) gentle introduction to event cameras][a brief introduction].
Instead, in this post I just want to share some advice I found useful during my
research, hopefully to inspire curiosity in other researchers, practitioners,
and entrepreneurs.

{{< figure src="/ox-hugo/litftingscarpellini_abstr.png" title="The problem: from a moving subject  to skeleton estimation" class="center" width="100%" >}}


### Open-source research {#open-source-research}
I'm convinced that Computer vision researchers and practitionares should direct
each other to increase the state-of-the-art in meaningful ways. To reach such a
goal, researchers should take a step down the ivy-tower. How? I believe the
first steps are **writing good-quality code** and **summarizing paper for the general
public**.

Open-source doesn't mean **low-quality**. Event-based vision is novel, very
novel; **the opencv for event-cameras** doesn't exist yet, although some are
working onto it. The Robotics and Perception Group (the university of Zurich and
ETH Zurich) is collecting papers implementation on their [github
page](https://github.com/uzh-rpg/event-based%5Fvision%5Fresources).
[Prophesee](https://www.prophesee.ai/) has a SDK for their event-cameras, but
the software is limited to its products.

As an attempt, I developed my own tiny library with some tools for
event-cameras. You can find it at
<https://github.com/IIT-PAVIS/event%5Flibrary>.


### Event-synthesis {#event-synthesis}

**Data** are the fuel of novel Deep Learning models. Continuing with the analogy to
oil, data are also extremely expensive to extract and elaborate. In particular,
datasets recorded with event-cameras are not comparable in size and variance to
the large RGB datasets. For these reasons, **event synthesis** is amazing. Recent
literature provides interesting results about generate synthetic events from RGB
images or videos ([Rebecq et al. 2019](#org1d5ad5b)).

I used my _event-library_ to generate synthetic events from a millions of RGB
frames of the standard Human3.6m dataset ([Ionescu et al. 2014](#org33ec73a)).

{{< figure src="/ox-hugo/h3m.png" title="Syntehtic events allow to recycle standard RGB datasets and test algorithms without using an event-camera" class="center" width="100%" >}}

I find this especially intriguing for entrepreneurs and engineers in automotive
and time-critical applications. Companies can convert their own data to
synthetic events in order to evaluate event-based algorithms before event
acquiring event-cameras (which are still expensive, although major companies
entering the field will lower costs).


### My research -- what about Human Pose Estimation? {#my-research-what-about-human-pose-estimation}

> _Only in code veritas._

You have certainly appreciated the results of "Human Pose Estimation" (also
called "Motion Capture") techniques. They are exploited in _Star Wars_, _Avatar_,
and major video-games to produce amazing special effect (some examples
<https://www.youtube.com/watch?v=bkvW9hsypHw>).

Motion Capture systems are based on specialize hardware and a large number of
synchronized cameras. In this conditions, motions at high speed are hard to
capture. My research looks for an answer to a common problem in this
applications: **elaborating data at high speed**. Event-cameras record movements at
high speed efficiently.

{{< figure src="/ox-hugo/liftingscarpellini_results.png" title="Motion Capture with an event-camera" class="center" width="100%" >}}


## Bibliography {#bibliography}

<a id="org33ec73a"></a>Ionescu, Catalin, Dragos Papava, Vlad Olaru, and Cristian Sminchisescu. 2014. “Human3.6m: Large Scale Datasets and Predictive Methods for 3d Human Sensing in Natural Environments.” _IEEE Transactions on Pattern Analysis and Machine Intelligence_ 36 (7):1325–39. <https://doi.org/10.1109/tpami.2013.248>.

<a id="org1d5ad5b"></a>Rebecq, Henri, René Ranftl, Vladlen Koltun, and Davide Scaramuzza. 2019. “High Speed and High Dynamic Range Video with an Event Camera.” _IEEE Trans. Pattern Anal. Mach. Intell. (T-PAMI)_. <http://rpg.ifi.uzh.ch/docs/TPAMI19%5FRebecq.pdf>.

[^fn:1]: Link at <https://tub-rip.github.io/eventvision2021/>
