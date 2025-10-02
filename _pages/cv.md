---
layout: page
permalink: /cv/
title: cv
nav: true
nav_order: 5
---

<div class="cv-container">
  <div class="cv-header" style="text-align: center; margin-bottom: 20px;">
    <p><a href="{{ '/assets/pdf/Yixuan_CV_20251002.pdf' | relative_url }}" target="_blank" class="btn btn-primary">📄 Download PDF</a></p>
  </div>
  
  <div class="cv-embed" style="width: 100%; height: 800px; border: 1px solid #ddd; border-radius: 8px;">
    <iframe 
      src="{{ '/assets/pdf/Yixuan_CV_20251002.pdf' | relative_url }}" 
      width="100%" 
      height="100%" 
      frameborder="0"
      style="border-radius: 8px;">
      <p>Your browser does not support PDFs. <a href="{{ '/assets/pdf/Yixuan_CV_20251002.pdf' | relative_url }}" target="_blank">Download the PDF</a>.</p>
    </iframe>
  </div>
</div>

<style>
  .cv-container {
    max-width: 900px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .btn {
    display: inline-block;
    padding: 10px 20px;
    background-color: var(--global-theme-color);
    color: white;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s;
  }
  
  .btn:hover {
    background-color: var(--global-hover-color);
    text-decoration: none;
    color: white;
  }
  
  @media (max-width: 768px) {
    .cv-embed {
      height: 600px !important;
    }
  }
</style>
