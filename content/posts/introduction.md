+++
title = "A gentle introduction to event cameras"
author = ["Gianluca Scarpellini"]
date = 2020-10-29T09:34:00+01:00
lastmod = 2020-10-29T10:07:10+01:00
tags = ["introduction", "event-cameras"]
draft = false
weight = 2001
noauthor = true
nocomment = true
nodate = true
nopaging = true
noread = true
+++

#### Introduction {#introduction}

Can computer see like we humans do? Computer vision is a joint branch of machine
learning, statistics, and computer science. It's main goal is providing
artificial agents (e.g., robots, autonomous cars, drones, surveilling systems)
the ability to **see** and **understand** the environment. Deep learning and machine
learning are contributing enormeously to computer vision. Open-source
implementations of the recent literature (e.g., torchvision, tensorflow,
recently opencv) demonstrate that deep learning applications are mature and
ready for industrial applications. The Pic below is an (abused) example of how fast
the community has grown during the past decade. Today, artificial agent perform
better than human on huge set of classes.

{{< figure src="/ox-hugo/old_joke.png" title="Old joke (not true anymore)" class="center" >}}

Is it all? Has computer vision reached complete maturity? I believe it's not.

Standard cameras suffer of major intrinsics issues which can hardly be solved -
high bandwidth, high power consumption, low dynamic range. Humans don't see
images at fixed frame rates. We process only the **changes** of our sourrindings,
avoiding to process again and again the statical part of the scene. Our approach
is faster and more efficient, as we don't process the same information multiple
times.

I praise the human vision system because Nature has always been a source of
inspiration for engineering. Could we rethink computer vision, taking source
from Nature?g **Event-cameras** (cameras based on **events**) could be the
answer. In the following paragraphs, I try to convince the reader of the
potentials of event-based vision applications. This article is structure as
follows. I present event-cameras, their principle of operations, and their
motivation. Next, I show some solutions to solve the main challenges of
event-based vision. And finally, I conclude with a what I believe its the key:
everyone can contribute.


#### Event-cameras {#event-cameras}

Traditional cameras collect light and, at fixed frame-rate, output a single
frame. This approach suffers, however, of severe limitations. If part of the
scene is static, each frame contains the **same** pixel information, and the data
becomes redundant. Consequently, standard cameras with high frame-rate produce a
prohibitive large amount of throughput---most of which redundant if no change
occurs---that no algorithm can efficiently process. These limitation leads to
other common issues in standard computer vision: narrowed dynamic range and
blooming. Each standard image is **digitalized** and stored with a finite range of
values (e.g., 256 values per channel). If the light varies abruptly in the
scene, the digitalization process loses much of the information to fit into the
fixed range. Consequently, traditional cameras have a narrow dynamic range,
especially in automotive applications. For example, the sun in front of the
driver is a problematic issue for a standard camera. Moreover, if the incoming
light is too much, as in the after-mentioned example, the pixels saturate and
the resulting image is **burned**.

{{< figure src="/ox-hugo/me.png" title="This is me saying \"hello\"" class="center" >}}

The amateur photographer is aware of these issues and can use these
characteristics to create more artistic photo. On the other hand, computer
vision algorithms must be **reliable**, not artistic, and their reliability is
under attack in dynamic scenarios or when sources of lights are present in the
scene.

Can we rethink computer vision?

This question lead us to the central idea of event-cameras and its
paradigm. Event-cameras capture **change of intensities** (also called events) in
an asynchronous manner. Each event has 4 values: the position tuple on the image
plane (x, y), the polarity of the change (positive or negative), and the
timestamp of the its occurrence. This paradigm shift leads to some interesting
advantages. First of all, since each pixel work independently, event-cameras are
more robust against strong light changes. When the pixel of a standard camera
receives too much light intensity (e.g., if a camera is mounted on a car heading
west at dawn), it "flows" into the neighborhood pixels (**blooming effect**). On
the other hand, pixels of event-cameras don't store intensity values: events are
spiked immediately when a threshold is reached. No blooming happens, and dynamic
range is extremely high (140 dB vs 60 dB of traditional cameras). As you can
imagine, if each pixel transmit **only** the intensity changes, the
bandwidth---the amount of transmitted data---stays very low, while the
rate---the speed of data transmission---grows over 1 million events per
second. Consequently, events paradigm is for vision what oil is for energy:
efficient, rapid, and flexible. These interesting characteristics made
event-cameras the best available solution for robotics platform, intrusion
detection, and fast movement tracking. Events data preserve privacy of the
monitored space as well, because no subjects' details (e.g., face, eyes, and so
on) are captured. Major competitors&nbsp;[^fn:1] are exploring
low-cost event-based applications for intrusion detection.

{{< figure src="/ox-hugo/sphere_comparison.png" title="How does it work?" class="center" >}}

Where do the disadvantages lay?

Event-cameras detect only the movements and transmit asynchronous data. If the
scene is static, like in a beautiful mountain panorama, the only events are
noise. This new way of imaging makes events data incompatible with existing
computer vision applications. Moreover, deep learning models rely on
**synchronous** tensor representation, therefore even the **deep learning
revolution** is not directly available for event cameras.


#### Solutions {#solutions}

If you were looking for the Saint Grail of computer vision, look somewhere
else. They are not. Event-cameras are novel, expensive sensors---especially if
you are a first-time practitionares in computer vision. A huge effort is still
required to unlock their potential. I want to send this message clearly:
everyone can participate. Research in computer vision---and in many other fields
of compute science---needs fresh ideas. What makes event-cameras hard to employ
also makes them **exciting**---we are explorer looking for new, more efficient
paths.

What do we need?

The first thing we need are **data**. How could we exploit event-cameras
otherwise? Dataset collection is boring and hard, but necessary. There are
other, more interesting paths worth noting. The first is **domain adaptation**. We
could train on simulated dataset; **if it doesn't work in simulation, it doesn't
work in the real world real**. Simulation could be a game changer in event-base
vision; we need standardize, easy-to-use simulators. They must be **open-source**
as everyone could contribute.

Scaramuzza and his team developed an open-source simulator
([Rebecq, Gehrig, and Scaramuzza 2018](#org18229e9)). This could be exploit to generate huge amount of
publicly available dataset, both with complete simulation or by converting
standard computer vision dataset to events data. They made their point in an
elegant way: they engineered an approach for **reconstructing** gray-scale images
from events ([Rebecq et al. 2020](#orgad3e8b6)). Their reconstruction is
smooth and clear even in impossible conditions---e.g., capturing a bullet moving
at 1,000 km/h. This should be clear by now: they could only achieve this amazing
reconstruction quality using **simulated data** for training.

We can group events together and use events as standard frames. Events frames
can be stacked in tensors and used as input for synchronous deep learning models
(e.g., CNN, ANN). Currently, representing events as frames is the most
common technique to exploit event-cameras. This approach increases, however,
bandwidth and redundancy, and its benefits are limited compared to standard
cameras. Asynchronous machine learning models---e.g., Spiking Neural
Network---and sparse CNN ([Messikommer et al., n.d.](#orge0f3284)) are fascinating
path of research.


#### WOW papers {#wow-papers}

I have a dream. I hope that, one day, computer vision researchers and
practitionares will direct each other to increase the state-of-the-art in
meaningful ways. To reach such a goal, researchers should take a step down the
ivy-tower and toward self-made students and college professors. How? I believe
the first steps are **writing good-quality code** and **summarizing paper for the
general public**.

Open-source doesn't mean **low-quality**. Event-based vision is novel, very novel;
**the opencv for event-cameras** doesn't exist yet. The Robotics and Perception
Group (the university of Zurich and ETH Zurich) is collecting papers
implementation on their [github page](https://github.com/uzh-rpg/event-based%5Fvision%5Fresources). [Prophesee](https://www.prophesee.ai/)---a really cool private
company---already has a SDK for their event-cameras, but the software is limited
to its products. Hopefully, we'll have a well-engineered open-source library to
work with event-cameras.

**WOW papers**---papers worth sharing and knowing---should come **keys on
hand**. This is mostly not the case. I want to change this path, and I'm not
alone. I'll summarize the most interesting---and occasional, the most badly
written---works in dedicated post, to show their strong and their weakness.

I'll strongly prefer papers with a released implementation. Only in code
**veritas**.


#### Conclusion {#conclusion}

I presented event-cameras and showed their advantages and their limits. I
discuss how and in what measures event-cameras could change computer vision
applications. In particular, I focused on application that necessistates low
bandwidth, high acquisition rates, and low power consumption. The range of
applications of event-camera is a broad one: from space applications, in which
low energy consumption is the key to pack lighter batteries and ultimately save
millions on budget, to autonomous driving, where blurring and overflowing are
still dangerous for the driver. The path toward exploiting event-based cameras
is clear. Realistic and easy-to-use simulators could save time and energy in
collecting data. A well-engineered event-based vision package, lets call it
OpenEV, would certaintly increase the interest of industries and practitionares,
especially if big players were backing the project (we'll see, Samsung and Sony
have already shown their interest). If I made you more curious, kudos to me! I
refer you to ([Gallego et al. 2020](#org0764e08)) ---a fantastic and exhaustive overview of
event-cameras from some the **dragons** of the field.


## Bibliography {#bibliography}

<a id="org0764e08"></a>Gallego, Guillermo, Tobi Delbruck, Garrick Michael Orchard, Chiara Bartolozzi, Brian Taba, Andrea Censi, Stefan Leutenegger, et al. 2020. “Event-Based Vision: A Survey.” _IEEE Transactions on Pattern Analysis and Machine Intelligence_. Institute of Electrical and Electronics Engineers (IEEE), 1. <http://dx.doi.org/10.1109/TPAMI.2020.3008413>.

<a id="orge0f3284"></a>Messikommer, Nico, Daniel Gehrig, Antonio Loquercio, and Davide Scaramuzza. n.d. “Event-Based Asynchronous Sparse Convolutional Networks.” <https://youtu.be/LauQ6LWTkxM?t=4>.

<a id="org18229e9"></a>Rebecq, Henri, Daniel Gehrig, and Davide Scaramuzza. 2018. “ESIM: An Open Event Camera Simulator.” <https://www.blender.org/>.

<a id="orgad3e8b6"></a>Rebecq, Henri, Rene Ranftl, Vladlen Koltun, and Davide Scaramuzza. 2020. “High Speed and High Dynamic Range Video with an Event Camera.” _IEEE Transactions on Pattern Analysis and Machine Intelligence_ nil (nil):1. <https://doi.org/10.1109/tpami.2019.2963386>.

[^fn:1]: Samsung <https://www.samsung.com/au/smart-home/smartthings-vision-u999/>
