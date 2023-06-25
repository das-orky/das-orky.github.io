---
layout: single
author_profile: false 
classes: wide
sidebar:
  nav: "foo_project"
title: "Projects"
permalink: /project_home/
header:
  overlay_color: "#333"
  overlay_image: /assets/images/project_home_header.jpg
  overlay_filter: 0.3
  caption: "(CC) Creator: Denis_Azarenko"

excerpt: >
  All my projects belong to you now.<br />
  
feature_row_left:
  - image_path: /assets/images/project_1.jpg
    alt: "Scalable Human Genome Sequence Analysis"
    title: "Scalable Human Genome Sequence Analysis"
    excerpt: "A NSF project to create a large-scale genome analysis framework for Fabric testbed (underdevelopment)"
    url: "https://github.com/MU-Data-Science/GAF"
    btn_class: "btn--info"
    btn_label: "Learn more"
  - image_path: /assets/images/project_2.jpg
    alt: "Deep Network Based Naive Peak Caller"
    title: "Deep Network Based Naive Peak Caller"
    excerpt: "A deep neural network based classification model to identify enriched regions of a DNase-seq experiment."
    url: "https://github.com/das-orky/naive_peak_caller"
    btn_class: "btn--info"
    btn_label: "Learn more"
  - image_path: /assets/images/project_3.jpg
    alt: "Explainability"
    title: "Explainability"
    excerpt: "Anthropomorphising the output of a deep learning model. To untangle the reasoning behaviour of the model to call a region enriched or not."
    url: "https://github.com/das-orky/Explainability"
    btn_class: "btn--info"
    btn_label: "Learn more"      
  - image_path: /assets/images/project_4.jpg
    alt: "Darth Yader"
    title: "Darth Yader"
    excerpt: "Yet Another Downloader for ENCODE and Roadmap project. With emphasis on removing samples with extremely low spot score and read depth, etc., because high(good) quality data is vital for any machine technique. Bad data may lead you to the dark side."
    url: "https://github.com/das-orky/Darth_Yader"
    btn_class: "btn--info"
    btn_label: "Learn more" 
  - image_path: /assets/images/project_5.jpg
    alt: "Chromatin Accessibility"
    title: "Chromatin Accessibility"
    excerpt: "Re-implemented from scratch the Basset technique for identifying functional activity of a DNA sequence. The implementation is done with Pytorch, as opposed to the author's tensorflow implementation."
    url: "https://github.com/das-orky/Basset_DNA_accessibility"
    btn_class: "btn--info"
    btn_label: "Learn more" 
  - image_path: /assets/images/project_6.jpg
    alt: "Fast 2D Continuous Wavelet Transform"
    title: "Fast 2D Continuous Wavelet Transform"
    excerpt: "Implemented continuous wavelet transform with openMP and MPI interface for speed up in CPUs. Also a CUDA implementation for speed up in GPUs."
    url: "https://github.com/0rky/CWT"
    btn_class: "btn--info"
    btn_label: "Learn more" 
  - image_path: /assets/images/project_7.jpg
    alt: "Deep Neural Network Zoo"
    title: "Deep Neural Network Zoo"
    excerpt: "Implementation of models that introduce some innovative shifts in ideas. All the models are implemented using Pytorch."
    url: "https://github.com/das-orky/dnn_zoo"
    btn_class: "btn--info"
    btn_label: "Learn more" 
  - image_path: /assets/images/project_8.jpg
    alt: "Dstat for ubuntu 22.04"
    title: "Dstat for ubuntu 22.04"
    excerpt: "Dstat is a popular package to monitor system performance. Now it is forked into another project. To still use dstat on newer versions of ubuntu this repo is created, that takes care of dependency and bugs introduced via new ubuntu 22.04."
    url: "https://github.com/0rky/dstat"
    btn_class: "btn--info"
    btn_label: "Learn more" 
---

{% include feature_row id="feature_row_left" type="left" %}
