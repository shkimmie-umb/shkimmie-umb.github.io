---
layout: post
title: "Melanoma Detection with Uncertainty Quantification"
date: 2025-04-15
categories: [Medical AI, Computer Vision, Calibration]
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
  .hero-container {
    width: 100%; height: 180px; border-radius: 8px; margin-bottom: 25px;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden; position: relative; border: 1px solid #e1e4e8;
  }
  .hero-title {
    position: absolute; color: #2c3e50; font-size: 2.2em; font-weight: 800;
    z-index: 10; text-align: center; background: rgba(255, 255, 255, 0.95);
    padding: 15px 30px; border-radius: 8px; box-shadow: 0 4px 15px rgba(0,0,0,0.08);
  }
  .block-container {
    background: #fff; border: 1px solid #eaecef; border-radius: 8px;
    padding: 25px; margin-bottom: 30px;
  }
  .block-title { 
    font-weight: 700; font-size: 1.3em; color: #2c3e50; 
    margin-top: 0; margin-bottom: 15px; border-bottom: 2px solid #f6f8fa; padding-bottom: 8px; 
  }
  .badge-link { 
    text-decoration: none; color: white; padding: 10px 18px; border-radius: 6px; 
    font-weight: 600; display: flex; align-items: center; gap: 8px; transition: all 0.2s; 
  }
  .badge-link:hover { opacity: 0.9; transform: translateY(-1px); }
  .svg-panel {
    text-align: center; width: 100%; overflow: hidden;
  }
  .clickable-panel:hover {
    opacity: 0.95;
  }
</style>

<div id="vanta-bg" class="hero-container">
  <div class="hero-title">Melanoma Detection with Uncertainty Quantification</div>
</div>

<script>
VANTA.NET({ el: "#vanta-bg", mouseControls: true, touchControls: true, gyroControls: false, minHeight: 180.00, minWidth: 200.00, scale: 1.00, scaleMobile: 1.00, color: 0xb71c1c, backgroundColor: 0xffffff, points: 12.00, maxDistance: 20.00, spacing: 18.00 })
</script>

<div style="display: flex; gap: 15px; margin-bottom: 30px; flex-wrap: wrap;">
    <a href="https://arxiv.org/abs/2411.10322" target="_blank" class="badge-link" style="background-color: #b31b1b;"><i class="fas fa-file-pdf"></i> IEEE ISBI 2025 Paper</a>
    <a href="https://shkimmie-umb.github.io/plane-classifier-app/" target="_blank" class="badge-link" style="background-color: #ff9800; color: #fff; border: 2px solid #e65100; box-shadow: 0 0 10px rgba(255,152,0,0.3); font-size: 1.05em;"><i class="fas fa-microchip"></i> Edge Detector App</a>
    <a href="https://mpsych.org/melanoma" target="_blank" class="badge-link" style="background-color: #24292e;"><i class="fab fa-github"></i> GitHub Repo</a>
    <a href="https://mpsych.github.io/melanoma/" target="_blank" class="badge-link" style="background-color: #0366d6;"><i class="fas fa-globe"></i> Live Client App</a>
</div>

<div class="block-container">
  <div class="block-title">Conference Venue & Impact</div>
  <div class="svg-panel">
    <svg viewBox="0 0 850 140" style="width: 100%; max-width: 850px; height: auto;">
      <rect x="5" y="5" width="840" height="130" rx="8" fill="#f8f9fa" stroke="#e1e4e8" stroke-width="2"/>
      
      <rect x="25" y="25" width="180" height="90" rx="6" fill="#0d47a1"/>
      <text x="115" y="65" font-size="24" font-weight="900" fill="#ffffff" text-anchor="middle">IEEE ISBI</text>
      <text x="115" y="90" font-size="16" font-weight="bold" fill="#bbdefb" text-anchor="middle">2025</text>
      
      <text x="235" y="50" font-size="20" font-weight="bold" fill="#2c3e50">International Symposium on Biomedical Imaging</text>
      <text x="235" y="75" font-size="15" fill="#d32f2f" font-weight="600"><tspan fill="#495057">&#128205;</tspan> Houston, Texas, USA</text>
      
      <path d="M 235 95 L 820 95" stroke="#ced4da" stroke-width="1" stroke-dasharray="4"/>
      <text x="235" y="115" font-size="13" font-style="italic" fill="#1b5e20" font-weight="bold">
        &#9733; Premier IEEE flagship venue specializing in algorithmic breakthroughs for clinical vision & biomedical computation.
      </text>
    </svg>
  </div>
</div>

<div class="block-container">
  <div class="block-title">Paradigm Shift: Active Rejection Routing</div>
  <div class="svg-panel">
    <svg viewBox="0 0 850 200" style="width: 100%; max-width: 850px; height: auto;">
      <defs>
        <marker id="arr" viewBox="0 0 10 10" refX="6" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#495057"/></marker>
        <marker id="arr-g" viewBox="0 0 10 10" refX="6" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#2e7d32"/></marker>
        <marker id="arr-r" viewBox="0 0 10 10" refX="6" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#c62828"/></marker>
      </defs>

      <rect x="0" y="0" width="850" height="200" rx="8" fill="#f8f9fa" stroke="#eaecef"/>

      <circle cx="70" cy="100" r="35" fill="#4e342e" stroke="#2c3e50" stroke-width="2"/>
      <text x="70" y="155" font-size="14" font-weight="bold" text-anchor="middle" fill="#2c3e50">Ambiguous Lesion</text>
      <line x1="105" y1="100" x2="145" y2="100" stroke="#495057" stroke-width="2" marker-end="url(#arr)"/>

      <rect x="155" y="55" width="140" height="90" rx="8" fill="#e3f2fd" stroke="#1e88e5" stroke-width="2"/>
      <text x="225" y="95" font-size="15" font-weight="bold" text-anchor="middle" fill="#0d47a1">1,296 Models</text>
      <text x="225" y="115" font-size="11" text-anchor="middle" fill="#0d47a1">(10-Dataset Multi-Mix)</text>
      <line x1="295" y1="100" x2="335" y2="100" stroke="#495057" stroke-width="2" marker-end="url(#arr)"/>

      <rect x="345" y="55" width="160" height="90" rx="8" fill="#fff3e0" stroke="#fb8c00" stroke-width="2"/>
      <text x="425" y="95" font-size="15" font-weight="bold" text-anchor="middle" fill="#e65100">Entropy Filter</text>
      <text x="425" y="115" font-size="13" font-style="italic" text-anchor="middle" fill="#e65100">H(X) = -&Sigma; p log(p)</text>

      <path d="M 505 80 L 550 80 L 550 40 L 595 40" fill="none" stroke="#2e7d32" stroke-width="2" marker-end="url(#arr-g)"/>
      <path d="M 505 120 L 550 120 L 550 160 L 595 160" fill="none" stroke="#c62828" stroke-width="2" marker-end="url(#arr-r)"/>

      <rect x="605" y="15" width="220" height="50" rx="6" fill="#e8f5e9" stroke="#2e7d32" stroke-width="2"/>
      <text x="715" y="40" font-size="13" font-weight="bold" text-anchor="middle" fill="#1b5e20">Certain: Accept Prediction</text>
      <text x="715" y="55" font-size="11" text-anchor="middle" fill="#1b5e20">Retain Autonomous Pipeline</text>

      <rect x="605" y="135" width="220" height="50" rx="6" fill="#ffebee" stroke="#c62828" stroke-width="2"/>
      <text x="715" y="160" font-size="13" font-weight="bold" text-anchor="middle" fill="#b71c1c">Uncertain: Mark "Unknown"</text>
      <text x="715" y="175" font-size="11" text-anchor="middle" fill="#b71c1c">Route Directly to Dermatologist</text>
    </svg>
  </div>
</div>

<div class="block-container">
  <div class="block-title">Realized Performance Gains & Rejection Trajectory</div>
  
  <div class="svg-panel" style="margin-bottom: 25px;">
    <svg viewBox="0 0 850 140" style="width: 100%; max-width: 850px; height: auto;">
      <rect x="5" y="5" width="410" height="130" rx="10" fill="#e8f5e9" stroke="#81c784" stroke-width="2"/>
      <text x="210" y="75" font-size="55" font-weight="900" fill="#2e7d32" text-anchor="middle">+4.6%</text>
      <text x="210" y="105" font-size="18" font-weight="bold" fill="#1b5e20" text-anchor="middle">Accuracy Scaled</text>
      <text x="210" y="122" font-size="12" fill="#388e3c" text-anchor="middle">Baseline 93.2% &rarr; Optimized 97.8%</text>

      <rect x="435" y="5" width="410" height="130" rx="10" fill="#ffebee" stroke="#e57373" stroke-width="2"/>
      <text x="640" y="75" font-size="55" font-weight="900" fill="#c62828" text-anchor="middle">-40.5%</text>
      <text x="640" y="105" font-size="18" font-weight="bold" fill="#b71c1c" text-anchor="middle">Misdiagnoses Eradicated</text>
      <text x="640" y="122" font-size="12" fill="#d32f2f" text-anchor="middle">Confident False Positives/Negatives Prevented</text>
    </svg>
  </div>

  <div class="svg-panel">
    <svg viewBox="0 0 850 260" style="width: 100%; max-width: 850px; height: auto;">
      <rect x="5" y="5" width="840" height="250" rx="8" fill="#ffffff" stroke="#ced4da" stroke-width="1"/>
      
      <line x1="80" y1="50" x2="820" y2="50" stroke="#e9ecef" stroke-dasharray="4"/>
      <line x1="80" y1="110" x2="820" y2="110" stroke="#e9ecef" stroke-dasharray="4"/>
      <line x1="80" y1="170" x2="820" y2="170" stroke="#e9ecef" stroke-dasharray="4"/>
      <line x1="80" y1="230" x2="820" y2="230" stroke="#e9ecef"/>

      <text x="70" y="55" font-size="12" font-weight="bold" text-anchor="end" fill="#2e7d32">97.8%</text>
      <text x="70" y="115" font-size="12" text-anchor="end" fill="#495057">95.0%</text>
      <text x="70" y="175" font-size="12" text-anchor="end" fill="#495057">93.2%</text>
      <text transform="rotate(-90 25 140)" x="25" y="140" font-size="13" font-weight="bold" text-anchor="middle" fill="#2c3e50">Accuracy</text>

      <text x="80" y="250" font-size="12" text-anchor="middle" fill="#495057">0.0 (No Rejection)</text>
      <text x="450" y="250" font-size="12" text-anchor="middle" fill="#495057">0.10 Threshold</text>
      <text x="820" y="250" font-size="12" font-weight="bold" text-anchor="middle" fill="#2e7d32">0.20 (Optimal Rej)</text>

      <path d="M 80 170 C 250 140, 500 80, 820 50" fill="none" stroke="#1e88e5" stroke-width="4"/>
      
      <circle cx="80" cy="170" r="7" fill="#c62828"/>
      <text x="95" y="165" font-size="13" font-weight="bold" fill="#c62828">Uncalibrated: 93.2%</text>

      <circle cx="820" cy="50" r="8" fill="#2e7d32"/>
      <text x="700" y="35" font-size="14" font-weight="bold" fill="#2e7d32">Optimized Peak: 97.8%</text>
    </svg>
  </div>
</div>

<div class="block-container">
  <div class="block-title">Empirical Reliability Calibration (10-Bin Verification)</div>
  <div class="svg-panel">
    <svg viewBox="0 0 850 350" style="width: 100%; max-width: 850px; height: auto;">
      <rect x="100" y="10" width="650" height="280" fill="#ffffff" stroke="#ced4da"/>
      
      <line x1="100" y1="290" x2="750" y2="10" stroke="#adb5bd" stroke-width="2" stroke-dasharray="4"/>
      <text x="640" y="45" transform="rotate(-23 640 45)" font-size="12" font-weight="bold" fill="#495057">Perfectly Calibrated (y = x)</text>

      <line x1="100" y1="150" x2="750" y2="150" stroke="#f1f3f5"/>
      <line x1="425" y1="10" x2="425" y2="290" stroke="#f1f3f5"/>

      <text x="90" y="295" font-size="12" text-anchor="end" fill="#495057">0.0</text>
      <text x="90" y="155" font-size="12" text-anchor="end" fill="#495057">0.5</text>
      <text x="90" y="20" font-size="12" text-anchor="end" fill="#495057">1.0</text>
      <text transform="rotate(-90 40 150)" x="40" y="150" font-size="13" font-weight="bold" text-anchor="middle" fill="#2c3e50">True Outcomes</text>

      <text x="100" y="315" font-size="12" text-anchor="middle" fill="#495057">0.0</text>
      <text x="425" y="315" font-size="12" text-anchor="middle" fill="#495057">0.5</text>
      <text x="750" y="315" font-size="12" text-anchor="middle" fill="#495057">1.0</text>
      <text x="425" y="340" font-size="13" font-weight="bold" text-anchor="middle" fill="#2c3e50">Predicted Model Confidence</text>

      <path d="M 100 290 L 165 235 L 230 180 L 295 210 L 360 190 L 425 220 L 490 265 L 555 140 L 620 195 L 685 175 L 750 90" fill="none" stroke="#e57373" stroke-width="2"/>
      <circle cx="165" cy="235" r="3" fill="#c62828"/><circle cx="230" cy="180" r="3" fill="#c62828"/><circle cx="295" cy="210" r="3" fill="#c62828"/><circle cx="360" cy="190" r="3" fill="#c62828"/><circle cx="425" cy="220" r="3" fill="#c62828"/><circle cx="490" cy="265" r="3" fill="#c62828"/><circle cx="555" cy="140" r="3" fill="#c62828"/><circle cx="620" cy="195" r="3" fill="#c62828"/><circle cx="685" cy="175" r="3" fill="#c62828"/><circle cx="750" cy="90" r="3" fill="#c62828"/>

      <path d="M 100 290 L 165 260 L 230 230 L 295 190 L 360 170 L 425 150 L 490 135 L 555 105 L 620 80 L 685 60 L 750 30" fill="none" stroke="#2e7d32" stroke-width="2.5"/>
      <circle cx="165" cy="260" r="4" fill="#1b5e20"/><circle cx="230" cy="230" r="4" fill="#1b5e20"/><circle cx="295" cy="190" r="4" fill="#1b5e20"/><circle cx="360" cy="170" r="4" fill="#1b5e20"/><circle cx="425" cy="150" r="4" fill="#1b5e20"/><circle cx="490" cy="135" r="4" fill="#1b5e20"/><circle cx="555" cy="105" r="4" fill="#1b5e20"/><circle cx="620" cy="80" r="4" fill="#1b5e20"/><circle cx="685" cy="60" r="4" fill="#1b5e20"/><circle cx="750" cy="30" r="4" fill="#1b5e20"/>

      <rect x="120" y="30" width="260" height="65" rx="4" fill="#ffffff" stroke="#e1e4e8"/>
      <line x1="130" y1="48" x2="165" y2="48" stroke="#e57373" stroke-width="2"/><circle cx="147" cy="48" r="3" fill="#c62828"/>
      <text x="175" y="52" font-size="12" fill="#b71c1c" font-weight="bold">Single Dataset (Overconfident)</text>
      
      <line x1="130" y1="75" x2="165" y2="75" stroke="#2e7d32" stroke-width="2.5"/><circle cx="147" cy="75" r="4" fill="#1b5e20"/>
      <text x="175" y="79" font-size="12" fill="#1b5e20" font-weight="bold">10-Mix Multi-Backbone (Calibrated)</text>
    </svg>
  </div>
</div>

<div class="block-container">
  <div class="block-title">Curated Benchmark Breakthroughs</div>
  <div class="svg-panel">
    <svg viewBox="0 0 850 280" style="width: 100%; max-width: 850px; height: auto;">
      <rect x="5" y="5" width="410" height="125" rx="8" fill="#ffffff" stroke="#1e88e5" stroke-width="2"/>
      <rect x="5" y="5" width="120" height="125" rx="8" fill="#e3f2fd"/>
      <text x="65" y="60" font-size="16" font-weight="bold" fill="#0d47a1" text-anchor="middle">ISIC 2017</text>
      <text x="65" y="80" font-size="11" fill="#1e88e5" text-anchor="middle">DenseNet201</text>
      <text x="145" y="50" font-size="28" font-weight="900" fill="#2e7d32">91.9% Peak</text>
      <text x="145" y="80" font-size="13" font-weight="bold" fill="#c62828">-40.5% Misdiagnoses</text>
      <text x="145" y="105" font-size="11" fill="#6c757d">Brier Score Optimized to 0.0478</text>

      <rect x="435" y="5" width="410" height="125" rx="8" fill="#ffffff" stroke="#fb8c00" stroke-width="2"/>
      <rect x="435" y="5" width="120" height="125" rx="8" fill="#fff3e0"/>
      <text x="495" y="60" font-size="16" font-weight="bold" fill="#e65100" text-anchor="middle">ISIC 2018</text>
      <text x="495" y="80" font-size="11" fill="#fb8c00" text-anchor="middle">ResNet152</text>
      <text x="575" y="50" font-size="28" font-weight="900" fill="#2e7d32">95.8% Peak</text>
      <text x="575" y="80" font-size="13" font-weight="bold" fill="#c62828">-66.5% False Negatives</text>
      <text x="575" y="105" font-size="11" fill="#6c757d">ECE Score Crushed to 0.0103</text>

      <rect x="5" y="150" width="410" height="125" rx="8" fill="#ffffff" stroke="#8e24aa" stroke-width="2"/>
      <rect x="5" y="150" width="120" height="125" rx="8" fill="#f3e5f5"/>
      <text x="65" y="205" font-size="16" font-weight="bold" fill="#4a148c" text-anchor="middle">7-Point</text>
      <text x="65" y="225" font-size="11" fill="#8e24aa" text-anchor="middle">ResNet152</text>
      <text x="145" y="195" font-size="28" font-weight="900" fill="#2e7d32">87.5% Peak</text>
      <text x="145" y="225" font-size="13" font-weight="bold" fill="#c62828">Severe Outlier Mitigation</text>
      <text x="145" y="250" font-size="11" fill="#6c757d">ECE Down from 0.0396 &rarr; 0.0321</text>

      <rect x="435" y="150" width="410" height="125" rx="8" fill="#ffffff" stroke="#43a047" stroke-width="2"/>
      <rect x="435" y="150" width="120" height="125" rx="8" fill="#e8f5e9"/>
      <text x="495" y="205" font-size="16" font-weight="bold" fill="#1b5e20" text-anchor="middle">Kaggle</text>
      <text x="495" y="225" font-size="11" fill="#43a047" text-anchor="middle">ResNet101</text>
      <text x="575" y="195" font-size="28" font-weight="900" fill="#2e7d32">97.6% Peak</text>
      <text x="575" y="225" font-size="13" font-weight="bold" fill="#c62828">-81.0% False Negatives</text>
      <text x="575" y="250" font-size="11" fill="#6c757d">High-Risk Malignancy Routing Protected</text>
    </svg>
  </div>
</div>

<div class="block-container" style="margin-bottom: 0;">
  <div class="block-title">Zero-Upload Client-Side Edge Inference</div>
  <a href="https://shkimmie-umb.github.io/plane-classifier-app/" target="_blank" style="text-decoration: none; display: block;">
    <div class="svg-panel clickable-panel" style="transition: all 0.2s; cursor: pointer;">
      <svg viewBox="0 0 850 100" style="width: 100%; max-width: 850px; height: auto;">
        <rect x="5" y="5" width="840" height="90" rx="8" fill="#fff8e1" stroke="#ffb300" stroke-width="2"/>
        
        <rect x="20" y="25" width="150" height="50" rx="6" fill="#ff9800"/>
        <text x="95" y="55" font-size="16" font-weight="bold" fill="#ffffff" text-anchor="middle">Edge Detector</text>

        <text x="195" y="42" font-size="15" font-weight="bold" fill="#e65100">Instantaneous Edge Computing Execution Engine &#128279;</text>
        <text x="195" y="65" font-size="13" fill="#495057">
          &#10003; Processes inference natively inside local browser memory via direct client-side execution—guaranteeing strict patient privacy via zero file uploads.
        </text>
      </svg>
    </div>
  </a>
</div>