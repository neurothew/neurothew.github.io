---
layout: default
title: Gallery
permalink: /gallery/
---
# Gallery

<div class="gallery-grid">
  <img src="/assets/gallery/DSC03253.jpg" alt="Butterfly" class="gallery-photo">
  <img src="/assets/gallery/DSC05276.jpg" alt="EastCoast" class="gallery-photo">
  <img src="/assets/gallery/DSC02760.jpg" alt="Butterfly" class="gallery-photo">
  <img src="/assets/gallery/DSC04826.jpg" alt="EastCoast" class="gallery-photo">
  <img src="/assets/gallery/DSC05248.jpg" alt="EastCoast" class="gallery-photo">
  <img src="/assets/gallery/DSC02753.jpg" alt="Butterfly" class="gallery-photo">
  <img src="/assets/gallery/DSC03173.jpg" alt="EastCoast" class="gallery-photo">
  <img src="/assets/gallery/DSC02200.jpg" alt="EastCoast" class="gallery-photo">
  <img src="/assets/gallery/DSC01913.jpg" alt="EastCoast" class="gallery-photo">
  <img src="/assets/gallery/DSC00146.jpg" alt="EastCoast" class="gallery-photo">
  <!-- Add more images as needed -->
</div>


<script>
window.addEventListener('load', function() {
    resizeGrid();
    window.addEventListener('resize', resizeGrid);
});

function resizeGrid() {
    const grid = document.querySelector('.gallery-grid');
    // Target the IMAGES directly
    const images = Array.from(grid.querySelectorAll('.gallery-photo'));
    
    // Settings
    const gap = 10; 
    const targetHeight = 500; 
    const containerWidth = grid.clientWidth;

    let currentRow = [];
    let currentWidth = 0;

    images.forEach((img) => {
        // Safety check: wait for image to load data
        if (img.naturalHeight === 0) return; 

        // Calculate aspect ratio
        const ratio = img.naturalWidth / img.naturalHeight;
        const widthAtTarget = targetHeight * ratio;

        currentRow.push({ img, widthAtTarget, ratio });
        currentWidth += widthAtTarget;

        // Check if the row is full
        if (currentWidth + (currentRow.length - 1) * gap > containerWidth) {
            
            const totalGaps = (currentRow.length - 1) * gap;
            const availableWidth = containerWidth - totalGaps;
            const totalRatio = currentRow.reduce((sum, item) => sum + item.ratio, 0);
            
            // Calculate perfect height for this row
            const newHeight = availableWidth / totalRatio;

            // Apply size to images
            currentRow.forEach(item => {
                item.img.style.height = `${newHeight}px`;
                item.img.style.width = 'auto'; // Browser handles width via Aspect Ratio
            });

            // Reset
            currentRow = [];
            currentWidth = 0;
        }
    });

    // Handle the last row (Stop it from stretching)
    currentRow.forEach(item => {
        item.img.style.height = `${targetHeight}px`;
        item.img.style.width = 'auto';
    });
}
</script>
