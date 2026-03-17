---
layout: page
title: Projects
permalink: /projects/
nav: true
nav_order: 4
mathjax: true
---

<style>
  .project-card {
    background: #fff;
    border: 1px solid #eaecef;
    border-radius: 8px;
    padding: 25px;
    margin-bottom: 30px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.04);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    border-left: 5px solid #bdc3c7;
  }
  .project-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(0,0,0,0.08);
  }
  .card-meta { border-left-color: #2196f3; }
  .card-plane { border-left-color: #27ae60; }
  .card-melanoma { border-left-color: #8e44ad; }
  
  .project-title {
    margin-top: 0;
    margin-bottom: 10px;
    font-size: 1.4em;
    color: #2c3e50;
  }
  .project-tags {
    margin-bottom: 15px;
    font-size: 0.85em;
    font-weight: 600;
    color: #7f8c8d;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .project-desc {
    font-size: 1.05em;
    line-height: 1.6;
    color: #495057;
    margin-bottom: 20px;
  }
  .btn-read {
    display: inline-block;
    padding: 8px 16px;
    background: #f8f9fa;
    color: #2c3e50;
    text-decoration: none;
    font-weight: 600;
    border: 1px solid #ced4da;
    border-radius: 4px;
    transition: all 0.2s;
  }
  .btn-read:hover {
    background: #e9ecef;
    border-color: #adb5bd;
  }
</style>

<p style="font-size: 1.1em; color: #555; margin-bottom: 40px;">
  My research focuses on bridging the gap between highly robust mathematical AI models and lightweight, system-level software engineering for clinical deployment. 
</p>

<div class="project-card card-meta">
  <div class="project-tags">Submitted: MICCAI 2026 | System Architecture | Transformer Optimization</div>
  <h2 class="project-title">Meta-D: Metadata-Driven Attention via Tₘₐₓ Routing</h2>
  <div class="project-desc">
    Engineered a deterministic routing framework for multi-modal brain tumor segmentation. By utilizing a Transformer Maximizer Tₘₐₓ to calculate entropy, the model actively severs attention to missing or corrupted data streams. This architectural shift achieved state-of-the-art accuracy while shedding <strong>24.1% of model parameters</strong> and dropping computational complexity to O(N).
  </div>
  <a href="/projects/meta-d" class="btn-read">Read Full Article &rarr;</a>
</div>

<div class="project-card card-plane">
  <div class="project-tags">Medical AI | Computer Vision | Live Web Deployment</div>
  <h2 class="project-title">Context-Aware 2.5D MRI Plane Classification</h2>
  <div class="project-desc">
    Solved the "near-skull" geometric ambiguity problem in MRI scans. Rather than utilizing heavy 3D volumetric networks, I architected a lightweight 2.5D Context-Aware Classifier that samples adjacent slices to learn local anatomical flow. This corrected metadata was gated into a tumor detection pipeline, reducing clinical misdiagnoses by <strong>33.3%</strong>.
  </div>
  <a href="/projects/mri-context-aware" class="btn-read">Read Full Article &rarr;</a>
</div>

<div class="project-card card-melanoma">
  <div class="project-tags">Accepted: IEEE ISBI 2025 | Uncertainty Quantification | Bayesian AI</div>
  <h2 class="project-title">Melanoma Detection via Uncertainty Quantification</h2>
  <div class="project-desc">
    Architected a 2D Bayesian uncertainty pipeline designed for mission-critical Out-of-Distribution (OOD) detection in dermatology. By dynamically filtering predictions based on low-confidence entropy scores, the model successfully slashed critical false-negative diagnostic failures by <strong>40.5%</strong>.
  </div>
  <a href="/projects/melanoma-uncertainty" class="btn-read">Read Full Article &rarr;</a>
</div>