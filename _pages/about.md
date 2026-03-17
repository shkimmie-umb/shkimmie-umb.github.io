---
layout: about
title: About
permalink: /
subtitle: Ph.D. Candidate & Research Engineer | Low-Level Systems + Medical AI

profile:
  align: right
  image: shk_pic.jpg
  image_circular: false
  more_info: >

selected_papers: true
social: false
---

[[Google Scholar]](https://scholar.google.com/citations?user=a-Jr59UAAAAJ&hl=en) | [[GitHub]](https://github.com/shkimmie-umb) | [[LinkedIn]](https://www.linkedin.com/in/sanghyuk-kim-469687182/)

I am a **Ph.D. Candidate** in Computer Science at the University of Massachusetts Boston, conducting research under Prof. [Daniel Haehn](https://danielhaehn.com/) in the [Machine Psychology Group](https://mpsych.org/).

My research bridges the gap between **theoretical Medical AI** and **production-grade Systems Engineering**. I specialize in **Volumetric Computer Vision (2.5D/3D)**, **Uncertainty Quantification**, and **Hardware-Aware AI Architectures**, backed by over four years of industrial experience in low-level OS kernel development.

Prior to my doctoral studies, I worked as a **Systems Kernel Engineer** at TmaxOS. There, I architected custom graphics kernels and GDI+ interfaces to bridge Linux/Windows ABIs—a rigorous systems background that now underpins my work in building scalable, reliable, and lightweight healthcare AI for cloud deployment.

---

<div style="background-color: #f8f9fa; border-left: 5px solid #2196f3; padding: 25px; margin: 30px 0; border-radius: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.05);">
    <h3 style="margin-top: 0; color: #0d47a1; font-size: 1.3em; display: flex; align-items: center; gap: 10px;">
        <i class="fas fa-microchip"></i> Featured Architecture: Meta-D (Tₘₐₓ Routing)
    </h3>
    
    <p style="margin-bottom: 12px; font-size: 1.05em;">
        <strong>The Infrastructure Bottleneck:</strong> Standard 3D medical transformers blindly force dense attention across all inputs. When clinical data streams are corrupted or missing, these models waste massive compute interpolating garbage data, resulting in overconfident hallucinations and $O(N^2)$ memory bloat.
    </p>
    <p style="margin-bottom: 12px; font-size: 1.05em;">
        <strong>The System Solution:</strong> I engineered <strong>Meta-D</strong>, a deterministic routing framework driven by a Transformer Maximizer ($T_{max}$) module. It calculates signal entropy in real-time, actively severing attention to corrupted modalities and dynamically routing compute only to valid features.
    </p>
    <p style="margin-bottom: 25px; font-size: 1.05em;">
        <strong>Quantitative Impact:</strong> Achieved state-of-the-art multi-modal 3D tumor segmentation (>91% Dice) while drastically reducing the system footprint—<strong>cutting model parameters by 24.1%</strong> and reducing computational complexity to $O(N)$. <em>(Submitted to MICCAI 2026)</em>.
    </p>

    <div style="text-align: left;">
        <a href="/projects/meta-d"
           style="background-color: #2196f3; color: white; padding: 12px 24px; text-decoration: none; border-radius: 5px; font-weight: bold; font-size: 0.95em; box-shadow: 0 4px 10px rgba(33, 150, 243, 0.3); transition: transform 0.2s; display: inline-flex; align-items: center; gap: 8px;">
            <i class="fas fa-chart-line"></i> View Architecture & Metrics
        </a>
    </div>
</div>

---

### Additional High-Impact Research

<ul style="line-height: 1.8; font-size: 1.05em; color: #2c3e50;">
  <li style="margin-bottom: 15px;">
    <a href="/projects/mri-context-aware" style="text-decoration: none; font-weight: 600; color: #2980b9;">Context-Aware 2.5D MRI Plane Classification:</a> Architected a lightweight 2.5D CNN framework that samples adjacent slice context to mathematically resolve ambiguous "near-skull" MRI edge cases. Gating this corrected metadata into downstream networks reduced clinical brain tumor misdiagnoses by <strong>33.3%</strong>.
  </li>
  <li style="margin-bottom: 15px;">
    <a href="/projects/melanoma-uncertainty" style="text-decoration: none; font-weight: 600; color: #2980b9;">Melanoma Detection via Uncertainty Quantification:</a> Developed a 2D Bayesian uncertainty pipeline capable of Out-of-Distribution (OOD) detection. By filtering low-confidence predictions, this architecture slashed critical false-negatives by <strong>40.5%</strong>. <em>(Accepted: IEEE ISBI 2025)</em>.
  </li>
  <li>
    <strong>Zero-Latency Clinical Deployment:</strong> Engineered a client-side JavaScript-injection plugin (Boostlet.js) to execute complex PyTorch inference pipelines directly in the browser, eliminating hospital server latency. <em>(Accepted: IEEE ISBI 2025)</em>.
  </li>
</ul>

<div style="margin-top: 30px; text-align: center;">
    <a href="/projects/" style="color: #555; font-weight: bold; text-decoration: none; border-bottom: 2px solid #ccc; padding-bottom: 2px; transition: color 0.2s;">View All Full Project Breakdowns &rarr;</a>
</div>