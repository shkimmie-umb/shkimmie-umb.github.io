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

[[Google Scholar]](https://scholar.google.com/citations?user=a-Jr59UAAAAJ&hl=en) [[GitHub]](https://github.com/shkimmie-umb?tab=repositories) [[LinkedIn]](https://www.linkedin.com/in/sanghyuk-kim-469687182/)

I am a **Ph.D. Candidate** in Computer Science at the University of Massachusetts Boston, conducting research under Prof. [Daniel Haehn](https://danielhaehn.com/) in the [Machine Psychology Group](https://mpsych.org/).

My research bridges the gap between **theoretical Medical AI** and **production-grade Systems Engineering**. I specialize in **Volumetric Computer Vision (2.5D/3D)** and **Uncertainty Quantification**, backed by over four years of industrial experience in low-level OS kernel development.

Prior to my doctoral studies, I worked as a **Systems Kernel Engineer** at TmaxOS. There, I architected custom graphics kernels and GDI+ interfaces to bridge Linux/Windows ABIs—a rigorous systems background that now underpins my work in building scalable, reliable healthcare AI.

---

<div style="background-color: #f8f9fa; border-left: 5px solid #2980b9; padding: 20px; margin: 30px 0; border-radius: 4px;">
    <h3 style="margin-top: 0; color: #2c3e50; font-size: 1.2em;">🌟 Featured Research: Context-Aware 2.5D MRI Model</h3>
    
    <p style="margin-bottom: 10px;">
        <strong>The Problem:</strong> Identifying the anatomical plane (Axial, Coronal, Sagittal) is standard for humans, but AI models fail on <strong>"near-skull" edge slices</strong>. These ambiguous images lack distinct features, leading to corrupted metadata and severe domain shift in large datasets.
    </p>
    <p style="margin-bottom: 10px;">
        <strong>Our Solution:</strong> We introduce a <strong>2.5D Context-Aware Classifier</strong>. Instead of heavy 3D networks, we use a lightweight model that samples adjacent slices to learn <em>local anatomical flow</em>. This provides just enough context to resolve ambiguity, achieving <strong>>99% accuracy</strong>.
    </p>
    <p style="margin-bottom: 20px;">
        <strong>Clinical Impact:</strong> By gating this corrected metadata into a tumor detection pipeline, we reduced clinical misdiagnoses by <strong>33.3%</strong>.
    </p>

    <div style="text-align: center;">
        <a href="https://shkimmie-umb.github.io/plane-classifier-app/" target="_blank"
           style="background-color: #27ae60; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold; font-size: 0.95em; box-shadow: 0 2px 5px rgba(0,0,0,0.2); transition: background 0.3s; display: inline-block;">
            🚀 Try Real-Time Web App
        </a>

        <a href="/projects/mri-context-aware"
           style="background-color: #2980b9; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold; font-size: 0.95em; box-shadow: 0 2px 5px rgba(0,0,0,0.2); transition: background 0.3s; display: inline-block;">
            📊 View Interactive Results
        </a>
    </div>

## </div>

### Research & Engineering Focus

- **Volumetric Medical Intelligence**:

  - [**Context-Aware MRI Analysis:**](/projects/mri-context-aware) Architected the 2.5D CNN framework described above. This work reduced downstream brain tumor misdiagnoses by **33.3%**.
  - [**Melanoma Detection:**](/projects/melanoma-uncertainty) Developed uncertainty quantification pipelines that reduced diagnostic error rates by **40.5%** (Accepted at **IEEE ISBI 2025**).

- **Full-Stack Research Deployment:**

  - I build "Zero-Install" clinical tools. I engineer client-side inference pipelines using **TensorFlow.js, React, and WebAssembly**, enabling complex PyTorch models to run directly in the browser with no server latency.
  - _Deployment:_ [**Real-Time MRI Plane Detector**](https://shkimmie-umb.github.io/plane-classifier-app/).

- **Systems & Kernel Optimization:** \* Optimizing high-performance computing tasks using C/C++ and OS internals (Linux/Win32) to ensure cross-platform operability for critical enterprise architecture.
<!-- `I will be presenting my latest work at IEEE ISBI 2025 (Houston, TX). Feel free to connect!` -->

<!-- ---
layout: about
title: About
permalink: /
subtitle: Investigating Medical Imaging + Systems Programming

profile:
  align: right
  image: shk_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >

# news: true # includes a list of news items
selected_papers: true # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page
---

[[google scholar]](https://scholar.google.com/citations?user=a-Jr59UAAAAJ&hl=en) [[github]](https://github.com/shkimmie-umb?tab=repositories) [[sanghyuk.kim001@umb.edu]](mailto:sanghyuk.kim001@umb.edu)

Hello. I am Sanghyuk Kim, a Ph.D. student in Computer Science at the University of Massachusetts Boston, working under the guidance of Prof. [Daniel Haehn](https://danielhaehn.com/) in the Machine Psychology Lab. My research bridges medical imaging and systems programming to drive innovative advancements in healthcare diagnostics.

Before my Ph.D., I gained over four years of professional experience in software engineering, specializing in graphics kernel development for Unix/BSD operating systems. This background now underpins my interdisciplinary focus on leveraging low-level systems software for healthcare applications, notably in melanoma detection.

My work explores the intersection of:

- [**Machine Learning with Uncertainty Quantification**](https://arxiv.org/abs/2411.10322): Developing pipelines that enhance diagnostic reliability in medical imaging. Recent work on melanoma detection achieved a 40.5% reduction in misdiagnoses, presented at [IEEE ISBI 2025](https://biomedicalimaging.org/2025/).
- **Medical Imaging and AI for Healthcare**: Leveraging systems programming to improve imaging diagnostics and reduce risks associated with AI hallucinations in critical settings.
- **Kernel-Level Programming**: Creating robust solutions like graphics kernels to improve cross-platform operability and efficiency, now applied to cutting-edge research in healthcare.

Currently, I’m investigating new methods to combine machine learning with systems programming, aiming to enhance medical imaging reliability and expand the frontiers of healthcare technology.

`I'll be attending IEEE ISBI 2025 (Houston, TX, USA). Feel free to connect!` -->
