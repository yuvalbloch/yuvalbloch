---
lang : "en"
title: " "
draft: false
omit_header_text: false

cascade:
  params:
    cover_dimming_class: ""        # disable Ananke's default dimming (e.g. bg-black-60)
    featured_image: '/assets/image_for_top1.png'
---

<style>
  header.cover {
    background: none !important;
  }



  header.cover .cover-image {
    display: none !important;
  }
main.main-content,
.section,
.article {
  background: transparent !important;
  padding-top: 0 !important;
  margin-top: 0 !important;
  box-shadow: none !important;
}
  body {
    background: url('/assets/image_for_top1.png') no-repeat center center fixed;
    background-size: cover;
    margin: 0;
    padding: 0;
  }
  .overlay {
    background-color: rgba(255, 255, 255, 0.85);
    padding: 4rem 2rem;
    max-width: 800px;
    margin: auto;
    border-radius: 12px;
  }
</style>

<div class="overlay">
  <div style="text-align: center; margin-bottom: 2rem;">
    <img src="/assets/me.jpeg" alt="Yuval Bloch" style="border-radius: 50%; width: 300px; height: 300px; object-fit: cover; border: 4px solid #ccc; box-shadow: 0 0 12px rgba(0,0,0,0.15);">
  </div>

  
  ## Yuval Bloch

  I'm a **computational ecologist** studying the dynamics of complex systems in nature.  
  My work combines **ecology**, **computer science**, and **epidemiology**.
  
 **Email**: yuvalblo@post.bgu.ac.il
 
  [Learn more →](/about)
</div>

