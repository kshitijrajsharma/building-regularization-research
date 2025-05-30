---
title: 'Building Footprint Regularization : From Vectorization to Deep Learning'
keywords:
- markdown
- publishing
- manubot
lang: en-US
date-meta: '2025-05-30'
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
  <meta name="dc.date" content="2025-05-30" />
  <meta name="citation_publication_date" content="2025-05-30" />
  <meta property="article:published_time" content="2025-05-30" />
  <meta name="dc.modified" content="2025-05-30T11:43:33+00:00" />
  <meta property="article:modified_time" content="2025-05-30T11:43:33+00:00" />
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
  <link rel="alternate" type="text/html" href="https://kshitijrajsharma.github.io/building-regularization-research/v/0a2f786ed41a895f637a31abd6fd0276fcdbf2fb/" />
  <meta name="manubot_html_url_versioned" content="https://kshitijrajsharma.github.io/building-regularization-research/v/0a2f786ed41a895f637a31abd6fd0276fcdbf2fb/" />
  <meta name="manubot_pdf_url_versioned" content="https://kshitijrajsharma.github.io/building-regularization-research/v/0a2f786ed41a895f637a31abd6fd0276fcdbf2fb/manuscript.pdf" />
  <meta property="og:type" content="article" />
  <meta property="twitter:card" content="summary_large_image" />
  <meta property="og:image" content="https://kshitijrajsharma.com.np/avatar.jpg" />
  <meta property="twitter:image" content="https://kshitijrajsharma.com.np/avatar.jpg" />
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
([permalink](https://kshitijrajsharma.github.io/building-regularization-research/v/0a2f786ed41a895f637a31abd6fd0276fcdbf2fb/))
was automatically generated
from [kshitijrajsharma/building-regularization-research@0a2f786](https://github.com/kshitijrajsharma/building-regularization-research/tree/0a2f786ed41a895f637a31abd6fd0276fcdbf2fb)
on May 30, 2025.
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




Geographic information systems (GIS) and cartographic applications typically require building footprints as precise vector polygons, rather than raster masks [@url:https://openaccess.thecvf.com/content/CVPR2022/html/Zorzi_PolyWorld_Polygonal_Building_Extraction_With_Graph_Neural_Networks_in_Satellite_CVPR_2022_paper.html]. Building footprint regularization refers to the process of refining raw building outlines (e.g. from remotely sensed imagery or LiDAR) into clean polygon shapes that conform to expected geometric constraints (such as orthogonal corners or aligned edges). The goal is to eliminate irregular artifacts (noisy jags, misalignments) while preserving the true shape, so that the footprints are cartographically suitable for maps.
A robust approach to obtain buildings in vector format is to first predict raster buildings using a neural network and then applying postprocessing that outputs polygons. The results achieved by conventional methods are either limited in terms of generalization
capacity (Zebedin et al., 2008; Cui et al., 2012; Tian and Reinartz, 2013) or are not restricted sufficiently to prior knowledge of regularity (Marcos et al., 2018; Gur et al., 2019; Hatamizadehet al., 2020; Zhao et al., 2021; Zorzi and Fraundorfer, 2023)[@doi:10.5194/isprs-annals-X-2-2024-217-2024].This review traces the evolution of footprint regularization methods from early vectorization algorithms in the 1990s through modern deep learning approaches in the 2020s.
We focus on 2D footprint outline techniques (planimetric building outlines) and exclude full 3D building reconstruction or roof modeling. Key developments and representative methods are discussed for each era, highlighting their algorithms, use cases, strengths, and limitations. We then compare traditional versus deep learning-based methods in terms of performance, flexibility, accuracy, and integration into GIS workflows. The review draws on peer-reviewed research and real-world implementations (including open-source tools and commercial pipelines) to provide a comprehensive perspective for remote sensing and GIS professionals.

## Geometric and Heuristic Methods ( 1990s - 2000s )
 
**Edge Detection and Line Fitting**: Early building extraction in the 1990s relied on low-level image processing and geometric heuristics. For example, Huertas and Nevatia (1988) developed a system to detect buildings in aerial images by finding rectangular clusters of edges (lines) and using shadow cues to distinguish buildings from other structures [@doi:10.3390/ijgi8040191] . Building polygons often consist of jagged lines. Guercke and Sester [@guercke2011] use Hough-Transformation ( Mathematically formalized by Duda, R.O., & Hart, P.E. (1972)) to refine such polygons.

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

**Model-Based Fitting and Constraints**: Beyond Hough transforms, researchers explored explicit shape fitting. Zebedin et al. (2008) introduced an approach to reconstruct building footprints by first detecting numerous line segments and then filtering and clustering these lines by orientation. Here initial lines are filtered by forming a histogram of orientation and then removing outliers. The filtered line directions are used to reconstruct the building with regular appearance. This approach is flexible, as it is not restricted to 90° angles.[@doi:10.5194/isprs-annals-X-2-2024-217-2024].

This flexibility to allow non-90° angles was a strength like the footprint could, in principle, follow a building that isn’t perfectly orthogonal but it still assumed buildings have a limited set of principal directions (which may not hold for very irregular architectures).

Other methods employed *snakes/active contours* and energy minimization to refine building shapes. For example, Fazan and Dal Poz (2013) applied an active contour model (snakes) to building roof images, optimizing an energy that favored straight edges and right-angle corners. While this improved initial detections, A drawback of the proposed method is that the weighting functions favor right angles and therefore only work for buildings with simple rectangular shapes [@doi:10.5194/isprs-archives-XLI-B3-555-2016].

He et al. (2014) combined data-driven edge detection with a global regularization step: they used an alpha shape algorithm to get an initial footprint from LiDAR point data, then a variant of Douglas–Peucker that was formulated as an energy minimization focusing on polygon complexity (number of vertices). The output was further processed in two modes one maximizing geometric accuracy, another maximizing topological simplicity to balance detail vs. regularity[@doi:10.5194/isprs-archives-XLI-B3-555-2016].

Energy Formulation : ( Basically way to formulate errors on those lines detected )
𝐸 = 𝛼𝐸𝑑𝑖𝑠𝑡 + 𝛽𝐸𝑎𝑛𝑔𝑙𝑒 + 𝛾𝐸𝑙𝑒𝑛𝑔𝑡ℎ 

![Workflow of building regularization using energy formulation by Albers (2016)](https://github.com/user-attachments/assets/10242f9e-9a77-4433-95d7-9ed0337936fa){#fig:energy-formulation height="3in"}

These model-fitting approaches introduced the idea of globally optimizing a footprint shape (e.g., via dynamic programming or least-squares) to satisfy regularity constraints.

**Strengths and Limitations**: Traditional methods were mostly computationally lightweight and interpretable. They often ran in a couple of sequential steps (edge detection, line grouping, polygon formation) and could be tuned by adjusting thresholds (for line length, angle tolerance, etc.) When assumptions held e.g., a building was clearly rectangular and image data was clean ,these methods produced very clean footprints. For instance, a study by Guercke & Sester showed that applying Hough-based regularization removed minor zig-zag artifacts and yielded impressively straight building edges.

However, these approaches struggled as building shapes grew more complex or data quality worsened. Irregular or curved buildings (round towers, L- or T-shaped footprints, etc.) did not fit neatly into a two-orientation assumption or a single rectangle model. Many algorithms were fragile: failing to detect a single key edge could cause entire sides of a polygon to be missed. They were also scenario-specific often tailored to isolated buildings with simple roofs and would require retuning for different environments or data sources. It is often said that while such classical methods work in some cases, they are “not applicable to many complex building structures” and they rely heavily on human-engineered features and parameters [@doi:10.3390/ijgi8040191].

In summary, the pre-2010s state-of-the-art could produce “regular” building outlines under favorable conditions, but lacked the robustness and generality needed for broad, automated mapping tasks. These limitations set the stage for machine learning, which promised to learn building shape patterns directly from data and reduce the need for ad hoc rules.

## Transition to Learning-Based Methods (2010s)

By the mid-2010s, the rise of deep learning fundamentally changed how building footprints were extracted. Instead of manually defining edges and shape rules, researchers began training convolutional neural networks (CNNs) to recognize buildings and output them in raster or vector form. The typical pipeline circa 2015–2017 was to use a semantic segmentation network (such as U-Net or DeepLab) to produce a binary mask of building pixels, then apply a vectorization algorithm to convert that mask into polygons [@url:https://element84.com/software-engineering/automated-building-footprint-extraction-part-3-model-architectures/].

This two-step approach : **CNN segmentation followed by geometric post-processing**  was a direct evolution of earlier workflows, swapping out hand-coded image filters for learned CNN features. For example, Marmanis et al. (2016) and Maggiori et al. (2017) mentioned that fully convolutional networks could outperform traditional techniques in detecting building regions from aerial images [@doi:10.3390/ijgi8040191].

Once a clean building mask was obtained, off-the-shelf polygonization (e.g., marching squares to trace outlines) and Douglas–Peucker simplification would yield a polygon vector. A problem with this approach is that semantic segmentation models are unable to delineate the boundaries between objects of the same class. This means that a single polygon will be drawn around a group of buildings that share walls, such as a block of rowhouses. To handle this case, the semantic segmentation model can be replaced with an instance segmentation model such as **Mask R-CNN**. This model generates a separate raster mask for each instance of a class that is detected [@url:https://element84.com/software-engineering/automated-building-footprint-extraction-part-3-model-architectures/]. Beyong which additional smoothing or regularization was needed, and many practitioners continued to apply tolerance-based simplification or mild “squaring” adjustments to make the polygons map-ready.

![Semantic Segmentation to Instance Segmentation Aprooaches , [Source](https://element84.com/software-engineering/automated-building-footprint-extraction-part-3-model-architectures/#:~:text=A%20popular%2C%20yet%20naive%20approach,is%20applied%20to%20the%20polygons) ](https://github.com/user-attachments/assets/8036b15c-4532-4f5d-a863-ce077a379580){#fig:segmentation-approaches height="3in"}

## Deep Structured Models (Active Contours)

A significant development in bridging classical regularization and deep learning was the integration of active contour models into neural networks. Marcos et al. (2018) introduced Deep Structured Active Contours (DSAC), a hybrid approach where a CNN learns to predict the parameters of an active contour that locks onto building edges . In their framework, the network output is not a raster, but rather coefficients that define the shape and tension of an active contour (snake) which then deforms to fit the building boundary. 

Gur et al. (2019) extended this concept by iteratively updating a polygon outline in an end-to-end trainable manner. Their pipeline starts with an approximate polygon (like a coarse outline of the building) and uses a neural network to repeatedly adjust the vertices, analogous to how one would iteratively relax an active contour. While effective, the polygons produced by Gur et al. were not explicitly enforced to be rectilinear the focus was on aligning to image evidence, not necessarily making right angles [@doi:10.5194/isprs-annals-x-2-2024-217-2024].

Hatamizadeh et al. (2020) proposed a multi-building active contour model: a CNN first predicts initial contours for many buildings in a scene, and then a learned energy function refines all of them simultaneously [@doi:10.5194/isprs-annals-x-2-2024-217-2024]. This allowed processing dense urban scenes with many buildings at once, something earlier active-contour methods (which often assumed one building at a time) didn’t handle. Hatamizadeh’s model was end-to-end (it directly outputs vector polygons from an image), but like its predecessors, its regularization was implicit it preferred smooth, compact shapes but did not guarantee, say, all angles = 90°.



### Recurrent Vertex Prediction (Polygon RNNs)

Instead of converting segmentation masks into polygons as a post-processing step, Recurrent Vertex Prediction models approach polygon extraction as a sequence prediction problem. In this framework, the model outputs a series of vertices one at a time, similar to writing out coordinate lists.

Polygon-RNN, first introduced by Castrejon et al. (2017) and later improved by Acuna et al. (2018) [@doi:10.1109/CVPR.2017.595; @doi:10.1109/ECCV.2018.00229], demonstrated that a recurrent neural network (RNN) could learn to draw object outlines by sequentially predicting polygon vertices, using image features to guide the process at each step.

A notable extension of this idea is **PolyMapper** [@doi:10.1109/CVPR.2019.01048], which integrates convolutional and recurrent modules in an end-to-end architecture. First, a CNN component (similar to Mask R-CNN) detects building instances and predicts coarse masks along with boundary and corner probability maps. Next, the most likely vertices from the corner map are selected and passed, together with image features, into an LSTM-based recurrent module. This module outputs vertices in sequence to trace the building outline, stopping when an end-of-sequence token is predicted, which signals the polygon should close.

![Comparison of output generated by instance segmentation and Polymapper , [source](https://element84.com/software-engineering/automated-building-footprint-extraction-part-3-model-architectures/#:~:text=A%20popular%2C%20yet%20naive%20approach,is%20applied%20to%20the%20polygons)](https://github.com/user-attachments/assets/f04e317d-754b-4c0f-a109-da2c8c6ff868){#fig:polymapper-approach height="3in"}


This approach has distinct advantages: the RNN can learn to skip over minor irregularities, resulting in cleaner and simpler polygons with fewer vertices. It can also learn to favor structural regularities, such as right angles, due to its exposure to training data. PolyMapper demonstrated that such models produce more regular and human-like building footprints than traditional instance segmentation pipelines.

However, this modeling approach brings complexity. The network must learn when to terminate the sequence (when to stop adding vertexes), and the loss function must account for sequence prediction dynamics. Early Polygon-RNN models also faced issues such as generating self-intersecting polygons or incorrectly ordering vertices unless constraints were explicitly enforced.

![Overview of PolyMapper for Building and Roads : [Source](https://element84.com/software-engineering/automated-building-footprint-extraction-part-3-model-architectures/#:~:text=A%20popular%2C%20yet%20naive%20approach,is%20applied%20to%20the%20polygons)](https://github.com/user-attachments/assets/a96421ac-94f7-47c2-a387-7ae0a4a6f701){#fig:polymapper-approach width="5in"}





## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>

