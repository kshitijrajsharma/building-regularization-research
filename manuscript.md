---
title: 'Building Footprint Regularization : From Vectorization to Deep Learning'
keywords:
- markdown
- publishing
- manubot
lang: en-US
date-meta: '2025-05-25'
author-meta:
- Kshitij Raj Sharma
header-includes: |
  <!--
  Manubot generated metadata rendered from header-includes-template.html.
  Suggest improvements at https://github.com/manubot/manubot/blob/main/manubot/process/header-includes-template.html
  -->
  <meta name="dc.format" content="text/html" />
  <meta property="og:type" content="article" />
  <meta name="dc.title" content="Building Footprint Regularization : From Vectorization to Deep Learning" />
  <meta name="citation_title" content="Building Footprint Regularization : From Vectorization to Deep Learning" />
  <meta property="og:title" content="Building Footprint Regularization : From Vectorization to Deep Learning" />
  <meta property="twitter:title" content="Building Footprint Regularization : From Vectorization to Deep Learning" />
  <meta name="dc.date" content="2025-05-25" />
  <meta name="citation_publication_date" content="2025-05-25" />
  <meta property="article:published_time" content="2025-05-25" />
  <meta name="dc.modified" content="2025-05-25T17:21:34+00:00" />
  <meta property="article:modified_time" content="2025-05-25T17:21:34+00:00" />
  <meta name="dc.language" content="en-US" />
  <meta name="citation_language" content="en-US" />
  <meta name="dc.relation.ispartof" content="Manubot" />
  <meta name="dc.publisher" content="Manubot" />
  <meta name="citation_journal_title" content="Manubot" />
  <meta name="citation_technical_report_institution" content="Manubot" />
  <meta name="citation_author" content="Kshitij Raj Sharma" />
  <meta name="citation_author_institution" content="Department of Geoinformatics, Paris Lodron University, Salzburg, Austria" />
  <meta name="citation_author_orcid" content="0000-0002-2123-3917" />
  <link rel="canonical" href="https://kshitijrajsharma.github.io/building-regularization-research/" />
  <meta property="og:url" content="https://kshitijrajsharma.github.io/building-regularization-research/" />
  <meta property="twitter:url" content="https://kshitijrajsharma.github.io/building-regularization-research/" />
  <meta name="citation_fulltext_html_url" content="https://kshitijrajsharma.github.io/building-regularization-research/" />
  <meta name="citation_pdf_url" content="https://kshitijrajsharma.github.io/building-regularization-research/manuscript.pdf" />
  <link rel="alternate" type="application/pdf" href="https://kshitijrajsharma.github.io/building-regularization-research/manuscript.pdf" />
  <link rel="alternate" type="text/html" href="https://kshitijrajsharma.github.io/building-regularization-research/v/05a28c6ce7c1df80037fabd95c66863522072173/" />
  <meta name="manubot_html_url_versioned" content="https://kshitijrajsharma.github.io/building-regularization-research/v/05a28c6ce7c1df80037fabd95c66863522072173/" />
  <meta name="manubot_pdf_url_versioned" content="https://kshitijrajsharma.github.io/building-regularization-research/v/05a28c6ce7c1df80037fabd95c66863522072173/manuscript.pdf" />
  <meta property="og:type" content="article" />
  <meta property="twitter:card" content="summary_large_image" />
  <link rel="icon" type="image/png" sizes="192x192" href="https://manubot.org/favicon-192x192.png" />
  <link rel="mask-icon" href="https://manubot.org/safari-pinned-tab.svg" color="#ad1457" />
  <meta name="theme-color" content="#ad1457" />
  <!-- end Manubot generated metadata -->
bibliography:
- content/manual-references.json
manubot-output-bibliography: output/references.json
manubot-output-citekeys: output/citations.tsv
manubot-requests-cache-path: ci/cache/requests-cache
manubot-clear-requests-cache: false
...






<small><em>
This manuscript
([permalink](https://kshitijrajsharma.github.io/building-regularization-research/v/05a28c6ce7c1df80037fabd95c66863522072173/))
was automatically generated
from [kshitijrajsharma/building-regularization-research@05a28c6](https://github.com/kshitijrajsharma/building-regularization-research/tree/05a28c6ce7c1df80037fabd95c66863522072173)
on May 25, 2025.
</em></small>



## Authors



+ **Kshitij Raj Sharma**
  <br>
    ![ORCID icon](images/orcid.svg){.inline_icon width=16 height=16}
    [0000-0002-2123-3917](https://orcid.org/0000-0002-2123-3917)
    · ![GitHub icon](images/github.svg){.inline_icon width=16 height=16}
    [kshitijrajsharma](https://github.com/kshitijrajsharma)
    · ![Mastodon icon](images/mastodon.svg){.inline_icon width=16 height=16}
    [\@krschap@mastodon.social](https://mastodon.social/@krschap)
    <br>
  <small>
     Department of Geoinformatics, Paris Lodron University, Salzburg, Austria
  </small>


::: {#correspondence}
✉ — Correspondence possible via [GitHub Issues](https://github.com/kshitijrajsharma/building-regularization-research/issues)

:::


## Abstract {.page_break_before}




Geographic information systems (GIS) and cartographic applications typically require building footprints as
precise vector polygons, rather than raster masks [@url:https://openaccess.thecvf.com/content/CVPR2022/html/Zorzi_PolyWorld_Polygonal_Building_Extraction_With_Graph_Neural_Networks_in_Satellite_CVPR_2022_paper.html]. Building footprint regularization refers to the process
of refining raw building outlines (e.g. from remotely sensed imagery or LiDAR) into clean polygon shapes that conform to
expected geometric constraints (such as orthogonal corners or aligned edges). The goal is to eliminate
irregular artifacts (noisy jags, misalignments) while preserving the true shape, so that the footprints are
cartographically suitable for maps
In many cases, regularization assumes buildings are rectilinear structures with predominantly 90° corners : an assumption that, while not universally true, holds for
most residential and industrial buildings. This review traces the evolution of footprint regularization
methods from early vectorization algorithms in the 1990s through modern deep learning approaches in the
2020s.

We focus on 2D footprint outline techniques (planimetric building outlines) and exclude full 3D
building reconstruction or roof modeling. Key developments and representative methods are discussed for
each era, highlighting their algorithms, use cases, strengths, and limitations. We then compare traditional
versus deep learning-based methods in terms of performance, flexibility, accuracy, and integration into GIS
workflows. The review draws on peer-reviewed research and real-world implementations (including open-
source tools and commercial pipelines) to provide a comprehensive perspective for remote sensing and GIS
professionals.

## Geometric and Heuristic Methods ( 1990s - 2000s )
 
**Edge Detection and Line Fitting**: Early building extraction in the 1990s relied on low-level image processing and geometric heuristics. For example, Huertas and Nevatia (1988) developed a system to detect buildings in aerial images by finding rectangular clusters of edges (lines) and using shadow cues to distinguish buildings from other structures [@doi:10.3390/ijgi8040191] . Building polygons often consist of jagged lines. Guercke and Sester [@guercke2011] use Hough-Transformation to refine such polygons.

Those approach and similar ones could identify simple rectangular building footprints, but often produced polygons with jagged (bearing in mind they don't take into account the building shape itself rather the outline), noisy outlines. To clean such outlines, researchers applied line simplification algorithms from cartography, notably the Ramer–Douglas–Peucker algorithm : to remove small zig-zags and reduce vertex count while approximating the shape (which is still used to the date) [@url:https://element84.com/software-engineering/automated-building-footprint-extraction-part-3-model-architectures/].

The Douglas–Peucker algorithm (originally from 1973) [@douglas1973] became a common post-processing step to “compress” or simplify building polygon geometry.

![A simple illustration of Douglas-Peucker algorithm](https://github.com/user-attachments/assets/d8a3f362-6fd0-4dfb-84e8-a686275c82c5?sanitize=true){#fig:douglas-peucker width="5in"}

Overall, early methods were largely rule-based: edges and corners were detected via image filters, and building shapes were assembled by connecting these primitives under geometric constraints defined by human experts.

**Regularization via Hough Transform**: By the 2000s, more sophisticated heuristics were introduced to enforce regularity in building outlines. A prominent tool was the Hough Transform for line detection. Hough transform is a feature extraction method used in image analysis. Hough transform can be used to isolate features of any regular curve like lines, circles, ellipses, etc. Hough transform in its simplest from can be used to detect straight lines in an image.[@url:https://medium.com/@st1739/hough-transform-287b2dac0c70]
For instance, Guercke and Sester (2011) proposed a footprint simplification method that takes an initial digitized outline (which might be jagged) and uses a Hough Transform to identify the dominant line orientations; close-to-collinear segments are merged and adjusted by least-squares to align with those dominant directions [@url:https://www.mdpi.com/2220-9964/8/4/191].

![Initial hough transofrmation line segment explained by Guercke and Sester (2011)](https://github.com/user-attachments/assets/505773d4-2f24-4c82-8a09-7a87297e5d06?sanitize=true){#fig:hough-transformation-line height="2in"}


The result is a cleaner, rectilinear footprint where spurious bends are straightened and most angles are ~90° or 180° [@doi:10.5194/isprs-annals-X-2-2024-217-2024]. Shiyong Cui et al. (2012) similarly applied the Hough transform to grouping line segments into two perpendicular families corresponding to a building’s principal directions . They constructed an initial graph of line segments, pruned edges that lacked image contrast (assuming they were false boundaries), and then detected closed cycles in the graph to form building polygons [@doi:10.5194/isprs-annals-X-2-2024-217-2024].

This yielded neatly rectangular footprints for buildings aligned to the two main axes, although the method was inherently limited to rectilinear structures. Tian and Reinartz (2013) extended the idea to allow two arbitrary dominant orientations (not necessarily parallel/perpendicular to the image axes), enabling footprints with an oblique alignment (e.g. buildings rotated on the ground) [@doi:10.5194/isprs-annals-X-2-2024-217-2024].

These Hough-based methods exemplify how prior knowledge of building shape (e.g. most buildings have parallel opposite walls and right-angle corners) was hard-coded into algorithms well before machine learning became common. The advantage was that the output polygons were regular by design : straight lines, right or consistent angles; making them immediately usable for mapping. However, the success of these methods depended on reliable low-level edge detection. In practice, missing or spurious line segments could cause incomplete or incorrect polygons.
Methods like Cui’s required a clear dominance of two perpendicular directions; complex or curved buildings, or those with more than two prevailing orientations, fell outside their scope. Hough transform is considered as a computational complex in terms of algorithm itself & often require postprocessing techniques like snapping/merging lines or form cycles to create valid polygons[@url:https://medium.com/@st1739/hough-transform-287b2dac0c70]

![A simple Hough transformation explaination](https://github.com/user-attachments/assets/358c6451-8978-4cba-9e81-697431ac72c4?sanitize=true){#fig:hough-transformation width="5in"}





## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>

