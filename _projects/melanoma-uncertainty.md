---
layout: post
title: "Melanoma Detection with Uncertainty Quantification"
date: 2025-01-01
---

<script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>

<div style="display: flex; gap: 15px; margin-bottom: 30px; flex-wrap: wrap;">
    <a href="https://arxiv.org/abs/YOUR_ARXIV_ID" target="_blank" 
       style="text-decoration: none; background-color: #b31b1b; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; display: flex; align-items: center; gap: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.2); transition: transform 0.2s;">
        <i class="fas fa-file-pdf"></i> ArXiv Preprint
    </a>
    <a href="https://github.com/mpsych/melanoma" target="_blank" 
       style="text-decoration: none; background-color: #24292e; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; display: flex; align-items: center; gap: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.2); transition: transform 0.2s;">
        <i class="fab fa-github"></i> View Code
    </a>
    <a href="https://mpsych.github.io/melanoma/" target="_blank" 
       style="text-decoration: none; background-color: #27ae60; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; display: flex; align-items: center; gap: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.2); transition: transform 0.2s;">
        <i class="fas fa-rocket"></i> Live Demo
    </a>
</div>

<style>
  .viz-container {
    background: #fff;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 40px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  }
  .viz-title {
    font-weight: 700;
    font-size: 1.25em;
    color: #2c3e50;
    margin-bottom: 15px;
    border-bottom: 2px solid #f0f0f0;
    padding-bottom: 10px;
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
  .elevator-pitch {
    background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%);
    border-left: 5px solid #c0392b;
    padding: 20px 25px;
    margin-bottom: 40px;
    border-radius: 4px;
    font-family: "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  }
</style>

<div class="elevator-pitch">
  <div style="font-weight: 800; text-transform: uppercase; font-size: 0.85em; letter-spacing: 1px; color: #7f8c8d; margin-bottom: 10px;">The Core Philosophy</div>
  <div style="font-size: 1.05em; line-height: 1.6; color: #2c3e50;">
    <p>
      [cite_start]<strong>The Problem:</strong> Deep learning models are powerful but often "confidently incorrect." In melanoma detection, a confident false negative (telling a patient they are fine when they have cancer) is catastrophic[cite: 267].
    </p>
    <p>
      <strong>Our Solution:</strong> It is safer for an AI to say <em>"I don't know"</em> than to guess wrong. We implemented an <strong>Entropy-Based Uncertainty Quantification</strong> framework. By measuring the model's confusion, we identify ambiguous cases and refer them to human experts instead of making a risky automated guess.
    </p>
    <p>
      <strong>The Result:</strong> By rejecting uncertain predictions, we improved accuracy from <strong>93.2% &rarr; [cite_start]97.8%</strong> and reduced clinical misdiagnoses by <strong>40.5%</strong>[cite: 255].
    </p>
  </div>
</div>

<div class="viz-container">
  <div class="viz-title">1. Methodology: Diversity & Calibration</div>
  <p>
    [cite_start]To build a robust generalist model, we combined <strong>10 open-source datasets</strong> (ISIC'16-'20, 7-point, PH2, etc.) and trained 24 different CNN architectures [cite: 330-331].
  </p>
  <p>
    We then used <strong>Calibration Curves</strong> and <strong>Expected Calibration Error (ECE)</strong> to find the exact "Reject Threshold"—the point where the model's uncertainty is too high to be trusted.
  </p>
  
  <div style="text-align: center; margin: 20px 0;">
    <img src="/assets/img/melanoma_fig4.jpg" alt="Figure 4: Calibration Curves" style="width: 100%; max-width: 800px; border-radius: 8px; border: 1px solid #ddd;">
  </div>

  <div class="viz-caption">
    [cite_start]<strong>Figure 4 Analysis[cite: 445]:</strong> Models trained on combined datasets (Right) align much closer to the ideal diagonal line ($y=x$) compared to single datasets (Left). 
    This allows us to trust the model's probability scores when calculating uncertainty.
  </div>
</div>

<div class="viz-container">
  <div class="viz-title">2. Impact: Reducing Misdiagnoses</div>
  <p>
    How much safer is the model? We compared the number of <strong>False Positives (FP)</strong> and <strong>False Negatives (FN)</strong> before and after applying our uncertainty rejection.
  </p>
  
  <div id="error-reduction-chart" style="width:100%;height:450px;"></div>

  <div class="viz-caption">
    [cite_start]<strong>Figure 5 Data [cite: 482-485]:</strong>
    <ul style="margin-top:5px; margin-bottom:0;">
        <li><strong>Overall:</strong> We prevented <strong>353 misdiagnoses</strong> across all test sets.</li>
        <li><strong>Kaggle Dataset:</strong> We reduced False Negatives (missing a cancer diagnosis) by <strong>81%</strong> (from 177 to 44).</li>
        <li><strong>Clinical Safety:</strong> The red bars (False Negatives) are significantly lower in the "With Rejection" group, minimizing the risk of missing malignant tumors.</li>
    </ul>
  </div>
</div>

<div class="viz-container">
  <div class="viz-title">3. System Overview</div>
  <p>
    Our pipeline integrates heterogeneous data, standardizes it, and adds a "Human-in-the-Loop" safety valve for uncertain cases.
  </p>
  
  <div style="text-align: center; margin: 20px 0;">
    <img src="/assets/img/melanoma_fig1.jpg" alt="Figure 1: System Overview" style="width: 100%; max-width: 800px; border-radius: 8px; border: 1px solid #ddd;">
  </div>

  <div class="viz-caption">
    [cite_start]<strong>Figure 1[cite: 311]:</strong> The workflow consists of (1) Data Integration, (2) Melanoma Recognition (CNNs), (3) Uncertainty Analysis (Entropy), and (4) Integration, where "Uncertain" cases are filtered out for human review.
  </div>
</div>

<script>
  // --- CHART: ERROR REDUCTION (Data from Paper Figure 5 / Table 3) ---
  // We use a Grouped Bar Chart to show Before vs. After
  
  // DATASETS
  var x_labels = ['ISIC 2017', 'ISIC 2018', '7-Point', 'Kaggle'];

  // BEFORE REJECTION (Standard Model)
  var trace_fp_before = {
    x: x_labels,
    y: [104, 229, 83, 33], // Values from Source 466, 456, 468, 474
    name: 'False Positives (Standard)',
    type: 'bar',
    marker: {color: '#bdc3c7'} // Grey
  };
  
  var trace_fn_before = {
    x: x_labels,
    y: [23, 26, 23, 177], // Values from Source 466, 457, 469, 462
    name: 'False Negatives (Standard)',
    type: 'bar',
    marker: {color: '#e6b0aa'} // Light Red
  };

  // AFTER REJECTION (Our Method)
  var trace_fp_after = {
    x: x_labels,
    y: [60, 96, 40, 15], // Values from Source 466, 467, 468, 474
    name: 'False Positives (Ours)',
    type: 'bar',
    marker: {color: '#7f8c8d'} // Dark Grey
  };

  var trace_fn_after = {
    x: x_labels,
    y: [11, 12, 9, 44], // Values from Source 466, 467, 469, 475
    name: 'False Negatives (Ours)',
    type: 'bar',
    marker: {color: '#c0392b'} // Dark Red (Highlighting Safety)
  };

  var layout_errors = {
    barmode: 'group',
    title: {text: 'Reduction in Diagnostic Errors (Lower is Better)', font: {size: 14}},
    yaxis: {title: 'Count of Errors'},
    margin: {t: 40, b: 40, l: 50, r: 20},
    legend: {orientation: "h", y: 1.1}
  };

  Plotly.newPlot('error-reduction-chart', [trace_fp_before, trace_fn_before, trace_fp_after, trace_fn_after], layout_errors, {displayModeBar: false});
</script>