+++
title = "Lifting Monocular Events to 3D Human Poses"
author = ["Gianluca Scarpellini"]
lastmod = 2021-05-03T10:16:39+02:00
tags = ["event-cameras", "publications", "CVPRw"]
draft = false
weight = 1002
noauthor = true
nocomment = true
nodate = true
nopaging = true
noread = true
+++

## Abstract {#abstract}

This paper presents a novel 3D human pose estimation approach using a single
stream of asynchronous events as input. Most of the state-of-the-art approaches
solve this task with RGB cameras, which suffer when the subjects are moving
fast. On the other hand, event-based 3D pose estimation benefits from the
advantages of event-cameras, especially their efficiency and robustness to
appearance changes. Yet, finding human poses in asynchronous events is in
general more challenging than standard RGB pose estimation, since little or no
events are triggered in static scenes. Here we propose the first learning-based
method for 3D human pose from a single stream of events. Our method consists of
two steps. First, we process the event-camera stream to predict three orthogonal
heatmaps per joint; each heatmap is the projection of of the joint onto one
orthogonal plane. Next, we fuse the sets of heatmaps to estimate 3D localisation
of the body joints. As a further contribution, we make available a new,
challenging dataset for event-based human pose estimation by simulating events
from the RGB Human3.6m dataset. Experiments demonstrate that our method achieves
state-of-the-art accuracy, narrowing the performance gap between standard RGB
and event-based vision.

-   [Code](https://github.com/gianscarpe/event-based-monocular-hpe)
-   [Webpage](https://iit-pavis.github.io/lifting%5Fevents%5Fto%5F3d%5Fhpe/)
-   [Arxiv](https://arxiv.org/abs/2104.10609)


## BibTex citation {#bibtex-citation}

```text
@article{scarpellini2021lifting,
  title={Lifting Monocular Events to 3D Human Poses},
  author={Scarpellini, Gianluca and Morerio, Pietro and Del Bue, Alessio},
  journal={arXiv preprint arXiv:2104.10609},
  year={2021}
}
```
