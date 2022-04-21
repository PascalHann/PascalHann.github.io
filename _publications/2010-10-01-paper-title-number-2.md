---
title: "Incremental Updates of Path-Traced Scenes during Editing"
collection: publications
permalink: /publication/2022-04-01-Incremental-Updates-of-Path-Traced-Scenes-during-Editing
excerpt: 'In my bachelors thesis I present a novel algorithm for rerendering 3D scenes after it was changed by a user interaction.'
date: 2022-04-01
venue: ''
paperurl: 'https://www.cg.tuwien.ac.at/research/publications/2022/HANN_2022_IPT/HANN_2022_IPT-thesis.pdf'
citation: 'Pascal Hann, Hann. (2022). &quot;Incremental Updates of Path-Traced Scenes during Editing.&quot;'
---
In this work I present a novel adaptive sampling algorithm for 3D editing software, developed by me and my colleagues. The algorithm is based on the idea of using knowledge about how a given user interaction affects a scene visually. We split the image into regions and order them, according to that knowledge, from most noticeably affected to least. The rendering budget can then be focused on the more affected regions earlier and on the lesser ones later in an incremental rendering process. Although this concept could probably work with other rendering methods, we designed it to be able to use path-tracing as the viewport renderer in 3D editing software without the typical grain-like noise and waiting times for sufficiently smooth rendered images this technology usually comes with. The goal of this work is to offer users of 3D editing software an as uninterrupted workflow as possible while still being able to see their work in high quality.

[TU Vienna, Institute of Computer Graphics post](https://www.cg.tuwien.ac.at/research/publications/2022/HANN_2022_IPT/)

[Download paper here](https://www.cg.tuwien.ac.at/research/publications/2022/HANN_2022_IPT/HANN_2022_IPT-thesis.pdf)

Bibtex:

    @bachelorsthesis{HANN_2022_IPT,
    title =      "Incremental Updates of Path-Traced Scenes during Editing",
    author =     "Pascal Hann",
    year =       "2022",
    abstract =   "In this work I present a novel adaptive sampling algorithm
               for 3D editing software, developed by me and my colleagues.
               The algorithm is based on the idea of using knowledge about
               how a given user interaction affects a scene visually. We
               split the image into regions and order them, according to
               that knowledge, from most noticeably affected to least. The
               rendering budget can then be focused on the more affected
               regions earlier and on the lesser ones later in an
               incremental rendering process. Although this concept could
               probably work with other rendering methods, we designed it
               to be able to use path-tracing as the viewport renderer in
               3D editing software without the typical grain-like noise and
               waiting times for sufficiently smooth rendered images this
               technology usually comes with. The goal of this work is to
               offer users of 3D editing software an as uninterrupted
               workflow as possible while still being able to see their
               work in high quality.",
    month =      apr,
    address =    "Favoritenstrasse 9-11/E193-02, A-1040 Vienna, Austria",
    school =     "Research Unit of Computer Graphics, Institute of Visual
               Computing and Human-Centered Technology, Faculty of
               Informatics, TU Wien ",
    keywords =   "incremental rendering, path tracing, GPU",
    URL =        "https://www.cg.tuwien.ac.at/research/publications/2022/HANN_2022_IPT/",
    }