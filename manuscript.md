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
  <meta name="dc.modified" content="2025-05-25T14:40:55+00:00" />
  <meta property="article:modified_time" content="2025-05-25T14:40:55+00:00" />
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
  <link rel="alternate" type="text/html" href="https://kshitijrajsharma.github.io/building-regularization-research/v/0cad058848e4105ed6ca1a9421aab42b71f6c8e8/" />
  <meta name="manubot_html_url_versioned" content="https://kshitijrajsharma.github.io/building-regularization-research/v/0cad058848e4105ed6ca1a9421aab42b71f6c8e8/" />
  <meta name="manubot_pdf_url_versioned" content="https://kshitijrajsharma.github.io/building-regularization-research/v/0cad058848e4105ed6ca1a9421aab42b71f6c8e8/manuscript.pdf" />
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
([permalink](https://kshitijrajsharma.github.io/building-regularization-research/v/0cad058848e4105ed6ca1a9421aab42b71f6c8e8/))
was automatically generated
from [kshitijrajsharma/building-regularization-research@0cad058](https://github.com/kshitijrajsharma/building-regularization-research/tree/0cad058848e4105ed6ca1a9421aab42b71f6c8e8)
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
precise vector polygons, rather than raster masks [@url:https://openaccess.thecvf.com/content/CVPR2022/html/Zorzi_PolyWorld_Polygonal_Building_Extraction_With_Graph_Neural_Networks_in_Satellite_CVPR_2022_paper.html#:~:text=While%20most%20state,and%20polygonal%20angle%20difference%20loss]. Building footprint regularization refers to the process
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
 


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>

