---
layout: post
title: "Interactive Results: Context-Aware Plane Detection"
date: 2025-12-26
categories: [Medical AI, Computer Vision, System Engineering]
---

<script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
<script defer src="https://cdn.jsdelivr.net/npm/img-comparison-slider@8/dist/index.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/img-comparison-slider@8/dist/styles.css" />

<style>
  .viz-container {
    background: #fff;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 40px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  }
  .viz-header {
    border-bottom: 2px solid #f0f0f0;
    padding-bottom: 10px;
    margin-bottom: 15px;
  }
  .viz-title {
    font-weight: 700;
    font-size: 1.25em;
    color: #2c3e50;
    margin: 0;
  }
  .viz-caption {
    font-size: 0.9em;
    color: #555;
    margin-top: 15px;
    line-height: 1.5;
    background: #f9f9f9;
    padding: 10px;
    border-radius: 5px;
  }
  /* Elevator Pitch Styling */
  .elevator-pitch {
    background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%);
    border-left: 5px solid #2c3e50;
    padding: 20px 25px;
    margin-bottom: 40px;
    border-radius: 4px;
    font-family: "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  }
  .pitch-heading {
    font-weight: 800;
    text-transform: uppercase;
    font-size: 0.85em;
    letter-spacing: 1px;
    color: #7f8c8d;
    margin-bottom: 10px;
  }
  .pitch-text {
    font-size: 1.05em;
    line-height: 1.6;
    color: #2c3e50;
  }
</style>

<div class="elevator-pitch">
  <div class="pitch-heading">The Motivation</div>
  <div class="pitch-text">
    <p>
      <strong>The Ambiguity Problem:</strong> Identifying the anatomical plane (Axial, Coronal, Sagittal) of an MRI scan is usually easy—except at the edges. <strong>"Near-skull" edge images</strong> lack distinct anatomical features, making them inherently ambiguous for AI models and even human experts.
    </p>
    <p>
      <strong>The Consequence:</strong> Standard 2D classifiers fail on these ambiguous slices. This leads to corrupted metadata, confusing downstream tasks and causing domain shift when merging heterogeneous datasets.
    </p>
    <p>
      <strong>Our Solution:</strong> We introduce a <strong>Context-Aware 2.5D Model</strong>. By sampling adjacent slices, our model learns the <em>local anatomical flow</em>, providing just enough context to resolve ambiguity. This approach achieves <strong>>99% accuracy</strong> and corrects misclassifications that purely 2D models cannot solve.
    </p>
  </div>
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">1. Methodology: The 2.5D Context Pipeline</div>
  </div>
  <p>
    How do we teach a model to "see" context? We construct a 3-channel input where the center slice is the target, flanked by adjacent slices (Sequential) or random slices from the same volume (Random).
  </p>
  
  <div style="text-align: center; margin: 20px 0;">
    <img src="/Exp_images/Overview.png" alt="Figure 1: System Overview" style="width: 100%; max-width: 800px; border-radius: 8px; border: 1px solid #ddd;">
  </div>

  <div class="viz-caption">
    <strong>Figure 1 Overview:</strong> 
    (1) We aggregate heterogeneous data (2D & 3D sources). 
    (2) The 2.5D model learns a unified strategy, processing 2D images with static context and 3D images with dynamic context. 
    (3) The trained classifier generates missing metadata for any input slice.
  </div>
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">2. Quantitative Impact: Resolving Ambiguity</div>
  </div>
  <p>
    We compared a standard 2D baseline against our 2.5D approach on a mixed dataset. 
    The 2.5D model effectively eliminates errors in ambiguous classes.
  </p>
  <div id="main-accuracy-chart" style="width:100%;height:400px;"></div>
  <div class="viz-caption">
    <strong>Table 1 Results:</strong> While the 2D Baseline achieves 98.74%, it struggles with edge cases. 
    Adding 2.5D context (Random sampling) pushes performance to <strong>99.99%</strong> on the IXI test set, reducing misclassifications by <strong>60%</strong>.
  </div>
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">3. Visual Proof: Removing "Confident" Errors</div>
  </div>
  <p>
    The chart above shows <em>that</em> the model is better. This visualization shows <em>why</em>.
    Below shows the "Top-2 Most Confident Errors" made by the 2D model compared to our 2.5D model on the same difficult slices.
  </p>
  
  <div style="text-align: center; margin: 20px 0;">
    <img src="/Exp_images/Detectivework.png" alt="Figure 2: Top-2 Confident Errors per Class" style="width: 70%; max-width: 800px; border-radius: 8px; border: 1px solid #ddd;">
  </div>

  <div class="viz-caption">
    <strong>Figure 2 Analysis:</strong> 
    <br>
    <strong>Row 1 (Axial):</strong> The 2D model is confused by near-skull slices. The 2.5D model completely eliminates these errors.
    <br>
    <strong>Row 2 (Coronal):</strong> Large tumors cause asymmetry, fooling the 2D model into predicting "Sagittal". The 2.5D model uses context to correctly identify the plane despite the pathology.
  </div>
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">4. Ablation Study: The Importance of Sequential Context</div>
  </div>
  <p>
    To prove that the model is learning <em>anatomical flow</em> rather than just memorizing images, we trained on 3D volumes (IXI) and tested on an unseen 2D dataset (BRISC).
  </p>
  <div id="ablation-chart" style="width:100%;height:400px;"></div>
  <div class="viz-caption">
    <strong>Table 2 Results:</strong> In this challenging domain-shift scenario, the 2D model fails (48.7%). 
    However, <strong>Sequential Context (73.0%)</strong> outperforms Random Context, confirming that learning the sequential order of slices is key to resolving ambiguity.
  </div>
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">5. Application: Brain Tumor Detection</div>
  </div>

  <h4 style="margin-top:20px; color:#444;">A. Qualitative Analysis (Grad-CAM)</h4>
  <p>
    Before looking at the statistics, observe <em>how</em> the corrected metadata fixes the model's behavior.
    <strong>Left:</strong> Image-Only (Wrong). <strong>Right:</strong> Metadata-Enhanced (Correct).
  </p>
  <div style="max-width: 600px; margin: 0 auto 20px auto; border-radius: 8px; overflow: hidden; border: 1px solid #ddd;">
    <div style="text-align: center; margin: 20px 0;">
    <img src="/Exp_images/Gradcam.png" alt="Figure 2: Top-2 Confident Errors per Class" style="width: 70%; max-width: 800px; border-radius: 8px; border: 1px solid #ddd;">
    </div>
  </div>
  <div class="viz-caption">
    <strong>Figure 4 Analysis:</strong> The Image-Only model (left) focuses on background noise, incorrectly predicting Meningioma. 
    The Metadata-Enhanced model (right) correctly targets the tumor core, fixing the prediction to Glioma.
  </div>
  
  <h4 style="margin-top:40px; color:#444;">B. Quantitative Impact: Reducing Misdiagnoses</h4>
  <p>We applied this corrected attention to the full dataset using a <strong>Gated Strategy</strong> (filtering uncertain predictions).</p>
  <div id="misdiagnosis-chart" style="width:100%;height:350px;"></div>
  <div class="viz-caption" style="margin-bottom: 30px;">
    <strong>Figure 5 Results:</strong> The visual corrections translate to real numbers. The Image-Only model made 30 errors. 
    Using our Gated Metadata strategy reduced this to <strong>20 errors</strong>—a <strong>33.3% reduction</strong> in clinical misdiagnoses.
  </div>
</div>

<script>
  // --- CHART 1: MAIN MODEL ACCURACY (Table 1) ---
  var trace_main = {
    x: ['2D Baseline', '2.5D Sequential', '2.5D Random'],
    y: [98.74, 99.74, 99.74], 
    type: 'bar',
    text: ['98.74%', '99.74%', '99.74%'],
    textposition: 'auto',
    marker: { color: ['#bdc3c7', '#3498db', '#2980b9'] }
  };
  var layout_main = {
    yaxis: {title: 'Average Accuracy (%)', range: [98, 100]},
    margin: {t: 30, b: 40, l: 50, r: 20},
    title: {text: 'Model Accuracy (Resolving Ambiguity)', font: {size: 14}}
  };
  Plotly.newPlot('main-accuracy-chart', [trace_main], layout_main, {displayModeBar: false});

  // --- CHART 2: ABLATION STUDY (Table 2) ---
  var trace_ablation = {
    x: ['2D Reference', '2.5D Random', '2.5D Sequential'],
    y: [48.7, 63.5, 73.0], 
    type: 'bar',
    text: ['48.7%', '63.5%', '73.0%'],
    textposition: 'auto',
    marker: { color: ['#95a5a6', '#e67e22', '#d35400'] }
  };
  var layout_ablation = {
    yaxis: {title: 'Accuracy on Unseen Domain (%)', range: [40, 80]},
    margin: {t: 30, b: 40, l: 50, r: 20},
    title: {text: 'Robustness to Domain Shift', font: {size: 14}},
    annotations: [{
      x: 2, y: 73, text: "Sequential Context Critical",
      showarrow: true, arrowhead: 1, ax: 0, ay: -30
    }]
  };
  Plotly.newPlot('ablation-chart', [trace_ablation], layout_ablation, {displayModeBar: false});

  // --- CHART 3: TUMOR MISDIAGNOSIS (Figure 5) ---
  var trace_errors = {
    x: ['Image-Only', 'Metadata-Enhanced', 'Gated Metadata'],
    y: [30, 23, 20], 
    type: 'bar',
    text: ['30 Errors', '23 Errors', '20 Errors'],
    textposition: 'auto',
    marker: { color: ['#95a5a6', '#7f8c8d', '#c0392b'] }
  };
  var layout_errors = {
    yaxis: {title: 'Count of Misdiagnoses', range: [0, 35]},
    margin: {t: 30, b: 40, l: 50, r: 20},
    annotations: [{
      x: 2, y: 22, text: "<b>33.3% Reduction</b>",
      showarrow: true, arrowhead: 2, ax: 0, ay: -40, font: {color: '#c0392b', size: 14}
    }]
  };
  Plotly.newPlot('misdiagnosis-chart', [trace_errors], layout_errors, {displayModeBar: false});
</script>
<!-- ---
layout: post
title: "Context-Aware 2.5D MRI Intelligence: Solving the Metadata Crisis"
subtitle: "Reducing clinical diagnostic errors by 33% via automated geometric perception."
date: 2025-01-01
categories: [Medical AI, Computer Vision, System Engineering]
---

### 1. The Hidden Bottleneck in Medical AI
In clinical workflows, human radiologists instantly recognize the anatomical orientation (Axial, Coronal, Sagittal) of an MRI slice. However, automated AI systems rely heavily on metadata headers (DICOM/NIfTI).

**The Problem:** In large-scale heterogeneous datasets, these headers are frequently corrupted, missing, or inconsistent[cite: 98, 110].
* **Consequence:** When AI models blindly trust incorrect metadata, they fail.
* **The Gap:** Existing classifiers look at 2D slices in isolation, struggling with ambiguous "near-skull" slices that lack clear anatomical landmarks[cite: 114, 116].


### 2. The Solution: 2.5D Context-Aware Perception
I architected a **2.5D Context-Aware Convolutional Neural Network** that mimics how humans perceive volume. Instead of analyzing a single slice, the model leverages **multi-slice context**—sampling adjacent or random slices from the same volume to resolve geometric ambiguity[cite: 100, 118].

#### System Architecture
The pipeline aggregates heterogeneous 2D and 3D data sources, cleans them via morphological operations, and feeds them into a context-aware backbone (AlexNet/ResNet)[cite: 151, 153].


### 3. Key Performance Metrics
By moving from 2D to 2.5D, we achieved a drastic reduction in classification errors.

| Metric | 2D Standard Model | **2.5D Context-Aware (Ours)** | Improvement |
| :--- | :--- | :--- | :--- |
| **Accuracy** | 98.74% | **99.49%** | **+0.75%** |
| **Error Rate** | 1.26% | **0.51%** | **60% Reduction** |

*Data Source: Validation on BRISC and IXI datasets[cite: 102, 206].*

#### Visualizing the "Context" Advantage
In the qualitative analysis below, the 2D model confuses a Coronal slice with a Sagittal one due to a large asymmetric tumor. The 2.5D model uses context to ignore the asymmetry and correctly classify the plane[cite: 210, 212, 213].


### 4. Real-World Impact: Boosting Brain Tumor Detection
I didn't just build a classifier; I validated its utility in a downstream clinical task. We integrated this inferred metadata into a **Brain Tumor Detector** using a **Gated Uncertainty Strategy**.

* **Mechanism:** The system uses the metadata only when the classifier is confident (Low Predictive Entropy), filtering out noise[cite: 157, 159].
* **Result:** This strategy reduced tumor misdiagnoses by **33.3%**, improving accuracy from 97.0% to 98.0%[cite: 104, 237].

> **"The Metadata-Enhanced model correctly targets and predicts the tumor, whereas the Image-Only model generates false positives by focusing outside the brain."** [cite: 240, 241]

### 5. Engineering & Deployment (Full-Stack)
Research is useless if it sits in a PDF. I deployed this model as a **serverless, client-side web application** to ensure patient privacy and accessibility.

* **Tech Stack:** TensorFlow.js, React, WebAssembly.
* **Privacy:** Inference happens entirely in the user's browser; no medical data leaves the local machine[cite: 163, 164].
* **Status:** Open Source.

[**[View Live Demo]**](https://shkimmie-umb.github.io/plane-classifier-app/) | [**[GitHub Repository]**](https://mpsych.org/mri-plane)

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vanta@latest/dist/vanta.net.min.js"></script>

<div id="vanta-bg" style="width: 100%; height: 400px; margin-bottom: 20px; border-radius: 15px;"></div>

<script>
VANTA.NET({
  el: "#vanta-bg",
  mouseControls: true,
  touchControls: true,
  gyroControls: false,
  minHeight: 200.00,
  minWidth: 200.00,
  scale: 1.00,
  scaleMobile: 1.00,
  color: 0x3f51b5,       // Change to match your site theme
  backgroundColor: 0xffffff, // Change to match your background
  points: 15.00,
  maxDistance: 22.00,
  spacing: 18.00
})
</script> -->