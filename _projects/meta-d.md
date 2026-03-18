---
layout: post
title: "Meta-D: Metadata-Driven Attention via Transformer Maximizer (Tₘₐₓ) Routing"
date: 2026-03-15
categories: [Medical AI, System Engineering, Computer Vision]
---

<script defer src="https://cdn.jsdelivr.net/npm/img-comparison-slider@8/dist/index.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/img-comparison-slider@8/dist/styles.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vanta@latest/dist/vanta.net.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" />

<style>
  body {
    color: #2c3e50;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  }
  
  /* Hero Section */
  .hero-container {
    width: 100%; height: 250px; border-radius: 8px; margin-bottom: 30px;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden; position: relative; border: 1px solid #e1e4e8;
  }
  .hero-title {
    position: absolute; color: #2c3e50; font-size: 2.2em; font-weight: 800;
    z-index: 10; text-align: center; background: rgba(255, 255, 255, 0.9);
    padding: 15px 30px; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.08);
  }

  /* Split Visual Pitch Architecture */
  .vs-container {
    display: grid; grid-template-columns: 1fr 1fr; gap: 20px;
    margin-bottom: 40px;
  }
  .vs-panel {
    background: #ffffff; border: 1px solid #eaecef; border-radius: 8px;
    padding: 25px; box-shadow: 0 4px 12px rgba(0,0,0,0.04);
    display: flex; flex-direction: column; align-items: center; text-align: center;
  }
  .vs-header {
    font-size: 1.2em; font-weight: 700; margin-bottom: 20px;
    padding-bottom: 10px; border-bottom: 2px solid #f6f8fa; width: 100%;
  }
  .arch-node {
    padding: 12px 15px; border-radius: 6px; font-weight: 600; font-size: 0.9em;
    width: 180px; margin: 5px 0; z-index: 2; position: relative;
  }
  
  /* Conventional Colors */
  .node-input { background: #f8f9fa; border: 1px solid #ced4da; color: #495057; }
  .node-bad-input { background: #ffebee; border: 1px dashed #f44336; color: #b71c1c; }
  .node-dense { background: #fff3e0; border: 1px solid #ff9800; color: #e65100; padding: 20px 15px; }
  .node-error { background: #ffebee; border: 1px solid #f44336; color: #b71c1c; }
  
  /* Meta-D Colors */
  .node-tmax { background: #e3f2fd; border: 2px solid #2196f3; color: #0d47a1; padding: 20px 15px; box-shadow: 0 0 10px rgba(33, 150, 243, 0.2); }
  .node-success { background: #e8f5e9; border: 1px solid #4caf50; color: #1b5e20; }
  
  /* Connection Lines */
  .flow-down { font-size: 1.5em; color: #adb5bd; margin: 5px 0; }
  .flow-waste { font-size: 1.5em; color: #f44336; margin: 5px 0; }
  .flow-route { font-size: 1.5em; color: #4caf50; margin: 5px 0; }
  .flow-dense { font-size: 1.5em; color: #ff9800; margin: 5px 0; }
  
  .arch-desc { font-size: 0.9em; color: #6c757d; margin-top: 15px; line-height: 1.5; }

  /* Academic Tables */
  .table-container { margin-bottom: 40px; overflow-x: auto; }
  .academic-table {
    width: 100%; border-collapse: collapse; font-size: 0.95em;
    background: #fff; border: 1px solid #eaecef; border-radius: 8px; overflow: hidden;
  }
  .academic-table th {
    background: #f8f9fa; color: #2c3e50; font-weight: 700;
    text-align: left; padding: 15px; border-bottom: 2px solid #dee2e6;
  }
  .academic-table td {
    padding: 12px 15px; border-bottom: 1px solid #eaecef; color: #495057;
  }
  .academic-table tr:last-child td { border-bottom: none; }
  .highlight-row { background: #f1f8ff; font-weight: 600; color: #0366d6 !important; }

  /* Containers */
  .viz-container {
    background: #fff; border: 1px solid #eaecef; border-radius: 8px;
    padding: 30px; margin-bottom: 40px;
  }
  .viz-header { border-bottom: 2px solid #f6f8fa; padding-bottom: 10px; margin-bottom: 20px; }
  .viz-title { font-weight: 700; font-size: 1.4em; color: #2c3e50; margin: 0; }
  .badge-link { text-decoration: none; color: white; padding: 10px 20px; border-radius: 6px; font-weight: 600; display: flex; align-items: center; gap: 8px; transition: opacity 0.2s; }
  .badge-link:hover { opacity: 0.9; }

  /* Ensures the container allows horizontal scrolling on small screens */
  .table-container {
    margin-bottom: 40px;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
    border-radius: 8px;
  }

  /* Academic Table adjustments for responsiveness */
  .academic-table {
    width: 100%;
    min-width: 600px; /* Prevents the table from squishing below legibility */
    border-collapse: collapse;
    font-size: 0.95em;
    background: #fff;
  }

  /* Media Query for very small screens */
  @media screen and (max-width: 600px) {
    .academic-table {
      font-size: 0.8em; /* Slightly shrink font on mobile */
    }
    .viz-title {
      font-size: 1.2em; /* Shrink headers so they don't wrap awkwardly */
    }
  }
</style>

<div id="vanta-bg" class="hero-container">
  <div class="hero-title">Meta-D Architecture</div>
</div>

<script>
VANTA.NET({ el: "#vanta-bg", mouseControls: true, touchControls: true, gyroControls: false, minHeight: 200.00, minWidth: 200.00, scale: 1.00, scaleMobile: 1.00, color: 0x3f51b5, backgroundColor: 0xffffff, points: 14.00, maxDistance: 22.00, spacing: 18.00 })
</script>

<div style="display: flex; gap: 15px; margin-bottom: 30px; flex-wrap: wrap;">
    <a href="https://arxiv.org/abs/2603.04811" target="_blank" class="badge-link" style="background-color: #b31b1b;"><i class="fas fa-file-pdf"></i> ArXiv Preprint</a>
    <!-- <a href="#" target="_blank" class="badge-link" style="background-color: #24292e;"><i class="fab fa-github"></i> System Code (TBD)</a> -->
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">1. The Genesis: Curing Image-Only Blind Spots with Metadata</div>
  </div>
  
  <div style="background: #f8f9fa; padding: 20px; border-left: 4px solid #3498db; border-radius: 4px; margin-bottom: 25px;">
    <p style="font-size: 1.1em; line-height: 1.6; color: #2c3e50; margin-top: 0; margin-bottom: 12px;">
      <strong>The Hypothesis:</strong> Injecting clinical metadata into the pipeline should fundamentally improve tumor detection accuracy over standard image-only models.
    </p>
    <p style="font-size: 1.1em; line-height: 1.6; color: #2c3e50; margin-bottom: 12px;">
      <strong>The Visual Proof:</strong> After achieving higher F-1 scores, Grad-CAM visually confirmed <em>why</em>: metadata physically forces the network to stop guessing and shifts its attention directly onto the true tumor core.
    </p>
    <p style="font-size: 1.1em; line-height: 1.6; color: #2c3e50; margin-bottom: 0;">
      <strong>The Evolution:</strong> Proving that metadata outright cures 2D misclassifications became the foundation for scaling Meta-D to mathematically bypass entirely missing modalities in 3D space.
    </p>
  </div>

<div class="viz-caption">
    <strong>Figure 1:</strong> Grad-CAM visualization. The Image-Only baseline (left) guesses blindly based on artifacts. Meta-D modulation (right) physically pulls the network's attention back to the tumor core, curing the model's drawbacks.
  </div>
  
  <div style="text-align: center; margin: 30px 0;">
    <img src="/Exp_images/meta-d/gradcam.png" alt="Grad-CAM Attention Map Comparison" style="width: 75%; max-width: 900px; border-radius: 6px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); background: #f1f3f5; min-height: 350px; display: flex; align-items: center; justify-content: center; color: #adb5bd; font-weight: bold; border: 1px dashed #ced4da;">
  </div>


</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">2. Initial Validation: Brain Tumor Classification (Meta-D)</div>
  </div>
  <p style="font-size: 0.95em; color: #555; margin-bottom: 15px;">To quantify the visual evidence observed in the Grad-CAM analysis, the architecture was tested on a rigorous 2D classification task. By incrementally adding metadata context, the model effectively eliminates ambiguity in corrupted or edge-case slices.</p>
  <div class="table-container">
    <table class="academic-table" style="text-align: center;">
      <thead>
        <tr>
          <th rowspan="2" style="vertical-align: middle;">Dataset</th>
          <th rowspan="2" style="vertical-align: middle; text-align: center;">bias-<br>corr.</th>
          <th rowspan="2" style="vertical-align: middle; text-align: center;">2D Image<br>only</th>
          <th colspan="3" style="text-align: center; border-bottom: 1px solid #dee2e6;">Meta-D (Ours)</th>
        </tr>
        <tr>
          <th style="text-align: center;">Img + Seq</th>
          <th style="text-align: center;">Img + Plane</th>
          <th style="text-align: center;">Img + Seq + Plane</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td rowspan="2" style="vertical-align: top; text-align: left; font-weight: 600; padding-top: 12px;">BraTS 2020</td>
          <td rowspan="2" style="vertical-align: top; padding-top: 12px;">&#10003;</td>
          <td>0.9037 &plusmn; 0.0033</td>
          <td>0.9129 &plusmn; 0.0015</td>
          <td>0.9108 &plusmn; 0.0255</td>
          <td class="highlight-row"><strong>0.9138</strong> &plusmn; 0.0089</td>
        </tr>
        <tr>
          <td>0.9055 &plusmn; 0.0209</td>
          <td>0.9030 &plusmn; 0.0130</td>
          <td>0.9070 &plusmn; 0.0028</td>
          <td class="highlight-row"><strong>0.9099</strong> &plusmn; 0.0134</td>
        </tr>
        <tr>
          <td rowspan="2" style="vertical-align: top; text-align: left; font-weight: 600; border-top: 1px solid #dee2e6; padding-top: 12px;">BRISC</td>
          <td rowspan="2" style="vertical-align: top; border-top: 1px solid #dee2e6; padding-top: 12px;">&#10003;</td>
          <td style="border-top: 1px solid #dee2e6;">0.6890 &plusmn; 0.0226</td>
          <td style="border-top: 1px solid #dee2e6;">0.6860 &plusmn; 0.0622</td>
          <td style="border-top: 1px solid #dee2e6;">0.6955 &plusmn; 0.0118</td>
          <td class="highlight-row" style="border-top: 1px solid #dee2e6;"><strong>0.6989</strong> &plusmn; 0.0199</td>
        </tr>
        <tr>
          <td>0.6896 &plusmn; 0.0670</td>
          <td>0.6676 &plusmn; 0.0260</td>
          <td>0.6321 &plusmn; 0.0874</td>
          <td class="highlight-row"><strong>0.7016</strong> &plusmn; 0.0483</td>
        </tr>
        <tr>
          <td rowspan="2" style="vertical-align: top; text-align: left; font-weight: 600; border-top: 1px solid #dee2e6; padding-top: 12px;">BRISC<br>(skull-stripped)</td>
          <td rowspan="2" style="vertical-align: top; border-top: 1px solid #dee2e6; padding-top: 12px;">&#10003;</td>
          <td style="border-top: 1px solid #dee2e6;">0.6986 &plusmn; 0.0393</td>
          <td style="border-top: 1px solid #dee2e6;">0.7091 &plusmn; 0.0988</td>
          <td style="border-top: 1px solid #dee2e6;">0.7116 &plusmn; 0.0479</td>
          <td class="highlight-row" style="border-top: 1px solid #dee2e6;"><strong>0.7248</strong> &plusmn; 0.0163</td>
        </tr>
        <tr>
          <td>0.7222 &plusmn; 0.0671</td>
          <td>0.6976 &plusmn; 0.0109</td>
          <td>0.7005 &plusmn; 0.0560</td>
          <td class="highlight-row"><strong>0.7233</strong> &plusmn; 0.0608</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<h3 style="margin-top: 10px; color: #2c3e50; margin-bottom: 15px; font-size: 1.5em;">3. The Core Innovation: Severing Computational Waste in 3D</h3>
<p style="font-size: 1.05em; line-height: 1.6; margin-bottom: 25px; color: #2c3e50;">
  Armed with the proof that metadata strictly governs attention in 2D space, we applied this exact routing logic to solve the much harder problem of entirely missing modalities in 3D environments.
</p>

<div class="vs-container">
  
  <div class="vs-panel">
    <div class="vs-header" style="color: #e65100;">Conventional Transformers</div>
    
    <div style="display: flex; gap: 10px; width: 100%; justify-content: center;">
      <div class="arch-node node-input"><i class="fas fa-check-circle" style="color:#4caf50;"></i> Valid Modality</div>
      <div class="arch-node node-bad-input"><i class="fas fa-times-circle"></i> Missing Modality</div>
    </div>
    
    <div style="display: flex; gap: 60px; justify-content: center; width: 100%; margin: 5px 0;">
      <div class="flow-dense"><i class="fas fa-long-arrow-alt-down"></i></div>
      <div class="flow-dense"><i class="fas fa-long-arrow-alt-down"></i></div>
    </div>
    
    <div class="arch-node node-dense" style="width: 80%;">
      <strong>Dense Self-Attention</strong><br>
      <small>Forces interpolation of all inputs</small>
    </div>
    
    <div style="display: flex; gap: 60px; justify-content: center; width: 100%; margin: 5px 0;">
      <div class="flow-waste"><i class="fas fa-arrow-down"></i></div>
      <div class="flow-waste"><i class="fas fa-arrow-down"></i></div>
    </div>
    
    <div class="arch-node node-error" style="width: 80%;">
      <i class="fas fa-exclamation-triangle"></i> <strong>O(N²) Complexity</strong><br>
      <small>Hallucinates Fake Boundaries</small>
    </div>
    
    <div class="arch-desc">Standard networks blindly allocate attention to all inputs, wasting compute by forcing connections to missing data and propagating overconfident false positives into the final output.</div>
  </div>

  <div class="vs-panel" style="border: 2px solid #2196f3; box-shadow: 0 8px 20px rgba(33, 150, 243, 0.1);">
    <div class="vs-header" style="color: #0d47a1;">Meta-D (Ours)</div>
    
    <div style="display: flex; gap: 10px; width: 100%; justify-content: center;">
      <div class="arch-node node-input"><i class="fas fa-check-circle" style="color:#4caf50;"></i> Valid Modality</div>
      <div class="arch-node node-bad-input"><i class="fas fa-times-circle"></i> Missing Modality</div>
    </div>
    
    <div style="display: flex; gap: 60px; justify-content: center; width: 100%; margin: 5px 0;">
      <div class="flow-down"><i class="fas fa-arrow-down"></i></div>
      <div class="flow-down"><i class="fas fa-arrow-down"></i></div>
    </div>
    
    <div class="arch-node node-tmax" style="width: 80%;">
      <i class="fas fa-microchip"></i> <strong><i>T<sub>max</sub></i> Routing Module</strong><br>
      <small>Calculates Entropy & Evaluates Metadata</small>
    </div>
    
    <div style="display: flex; gap: 40px; align-items: center; justify-content: center; width: 100%; margin: 5px 0;">
      <div class="flow-route"><i class="fas fa-arrow-down" style="margin-right: 20px;"></i></div>
      <div style="color: #f44336; font-weight: bold; font-size: 1.2em; display: flex; flex-direction: column; align-items: center;">
        <i class="fas fa-ban"></i>
        <small style="font-size: 0.6em;">Blocked</small>
      </div>
    </div>
    
    <div class="arch-node node-success" style="width: 80%;">
      <i class="fas fa-tachometer-alt"></i> <strong>O(N) Complexity</strong><br>
      <small>Extracts True Features Only</small>
    </div>

    <div class="arch-desc">Meta-D actively calculates signal integrity via <i>T<sub>max</sub></i>. It directly severs attention to corrupted data, dynamically routing computational power exclusively to valid features.</div>
  </div>
</div>

<div class="viz-container">
  <div class="viz-header">
    <div class="viz-title">4. Final Proof: 3D Segmentation Performance & Robustness</div>
  </div>
  <p style="font-size: 1.05em; line-height: 1.6; margin-bottom: 25px;">
    By treating corrupted 3D data as a deterministic routing problem rather than relying on deep feature interpolation, Meta-D completely breaks the standard scaling laws of medical vision models. It achieves state-of-the-art accuracy against heavy transformer baselines while drastically reducing the system footprint.
  </p>

  <h4 style="color: #2c3e50; margin-bottom: 10px;">Table 1: Architectural Comparison (Missing Modality Scenario)</h4>
  <div class="table-container">
    <table class="academic-table">
      <thead>
        <tr>
          <th>Model Architecture</th>
          <th>Computational Complexity</th>
          <th>Parameter Count (M)</th>
          <th>Overall Dice Score (%)</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>UNETR (Heavyweight Baseline)<sup><a href="https://arxiv.org/abs/2103.10504" target="_blank" style="text-decoration:none; color:#3498db;" title="Hatamizadeh et al., 2022">[1]</a></sup></td>
          <td>O(N²)</td>
          <td>102.1</td>
          <td>84.52</td>
        </tr>
        <tr>
          <td>MMFormer (Missing Modality Baseline)<sup><a href="https://arxiv.org/abs/2206.03713" target="_blank" style="text-decoration:none; color:#3498db;" title="Zhang et al., MICCAI 2022">[2]</a></sup></td>
          <td>O(N²)</td>
          <td>45.8</td>
          <td>86.72</td>
        </tr>
        <tr class="highlight-row">
          <td>Meta-D (Ours)</td>
          <td>O(N)</td>
          <td>34.7 <span style="color: #28a745; font-size: 0.85em;">(-24.1%)</span></td>
          <td>91.84 <span style="color: #28a745; font-size: 0.85em;">(+5.12%)</span></td>
        </tr>
      </tbody>
    </table>
  </div>

  <h4 style="color: #2c3e50; margin-bottom: 10px; margin-top: 35px;">Table 2: Comprehensive Missing Modality Robustness (BraTS 2018)</h4>
  <p style="font-size: 0.95em; color: #555; margin-bottom: 15px;">
    Beyond raw efficiency, Meta-D demonstrates absolute robustness. We rigorously evaluated the architecture against all 15 possible combinations of missing MRI sequences. In every single scenario, <i>T<sub>max</sub></i> metadata routing outperformed standard image-only interpolation by successfully ignoring the missing modalities.
  </p>
  <div class="table-container">
    <table class="academic-table" style="text-align: center;">
      <thead>
        <tr>
          <th colspan="4" style="text-align: center; border-bottom: 1px solid #dee2e6; border-right: 1px solid #dee2e6;">Modalities</th>
          <th rowspan="2" style="vertical-align: middle; text-align: center; border-right: 1px solid #dee2e6;">3D Image only</th>
          <th style="text-align: center; border-bottom: 1px solid #dee2e6;">Meta-D (Ours)</th>
        </tr>
        <tr>
          <th style="text-align: center;">FLAIR</th>
          <th style="text-align: center;">T1c</th>
          <th style="text-align: center;">T1</th>
          <th style="text-align: center; border-right: 1px solid #dee2e6;">T2</th>
          <th style="text-align: center;">Img + Seq</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>&#9679;</td><td>&#9675;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">82.80</td>
          <td class="highlight-row"><strong>83.38</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9679;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">71.85</td>
          <td class="highlight-row"><strong>73.98</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9675;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">68.95</td>
          <td class="highlight-row"><strong>74.07</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9675;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">81.34</td>
          <td class="highlight-row"><strong>83.78</strong></td>
        </tr>
        <tr>
          <td>&#9679;</td><td>&#9679;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">85.74</td>
          <td class="highlight-row"><strong>86.27</strong></td>
        </tr>
        <tr>
          <td>&#9679;</td><td>&#9675;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">85.38</td>
          <td class="highlight-row"><strong>85.76</strong></td>
        </tr>
        <tr>
          <td>&#9679;</td><td>&#9675;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">86.56</td>
          <td class="highlight-row"><strong>87.00</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9679;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">76.00</td>
          <td class="highlight-row"><strong>77.89</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9679;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">85.04</td>
          <td class="highlight-row"><strong>85.74</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9675;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">84.52</td>
          <td class="highlight-row"><strong>85.66</strong></td>
        </tr>
        <tr>
          <td>&#9679;</td><td>&#9679;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9675;</td>
          <td style="border-right: 1px solid #eaecef;">86.35</td>
          <td class="highlight-row"><strong>86.93</strong></td>
        </tr>
        <tr>
          <td>&#9679;</td><td>&#9679;</td><td>&#9675;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">87.46</td>
          <td class="highlight-row"><strong>87.88</strong></td>
        </tr>
        <tr>
          <td>&#9679;</td><td>&#9675;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">87.26</td>
          <td class="highlight-row"><strong>87.72</strong></td>
        </tr>
        <tr>
          <td>&#9675;</td><td>&#9679;</td><td>&#9679;</td><td style="border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-right: 1px solid #eaecef;">85.82</td>
          <td class="highlight-row"><strong>86.28</strong></td>
        </tr>
        <tr>
          <td style="border-bottom: 2px solid #dee2e6;">&#9679;</td><td style="border-bottom: 2px solid #dee2e6;">&#9679;</td><td style="border-bottom: 2px solid #dee2e6;">&#9679;</td><td style="border-bottom: 2px solid #dee2e6; border-right: 1px solid #eaecef;">&#9679;</td>
          <td style="border-bottom: 2px solid #dee2e6; border-right: 1px solid #eaecef;">87.72</td>
          <td class="highlight-row" style="border-bottom: 2px solid #dee2e6;"><strong>88.24</strong></td>
        </tr>
        <tr style="background-color: #f8f9fa; font-weight: bold;">
          <td colspan="4" style="text-align: center; border-right: 1px solid #eaecef;">Average</td>
          <td style="border-right: 1px solid #eaecef;">82.85</td>
          <td style="color: #0366d6;">84.04</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>