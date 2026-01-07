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
  <img src="/assets/gallery/DSC02753.jpg" alt="Butterfly" class="gallery-photo">
  <img src="/assets/gallery/DSC05248.jpg" alt="EastCoast" class="gallery-photo">
  <!-- Add more images as needed -->
</div>

<script>
window.addEventListener('load', function() {
    resizeGrid();
    window.addEventListener('resize', resizeGrid);
});

function resizeGrid() {
    const grid = document.querySelector('.gallery-grid');
    const images = Array.from(grid.querySelectorAll('img'));
    const gap = 10; // Must match your CSS gap
    const targetHeight = 500; // Your preferred height
    const containerWidth = grid.clientWidth;

    let currentRow = [];
    let currentWidth = 0;

    images.forEach((img, index) => {
        // Calculate the aspect ratio (naturalWidth / naturalHeight)
        const ratio = img.naturalWidth / img.naturalHeight;
        const widthAtTarget = targetHeight * ratio;

        currentRow.push({ img, widthAtTarget, ratio });
        currentWidth += widthAtTarget;

        // If adding this image exceeds width (plus gaps), process the row
        if (currentWidth + (currentRow.length - 1) * gap > containerWidth) {
            
            // Calculate how much we need to shrink the row to fit perfectly
            const totalGaps = (currentRow.length - 1) * gap;
            const availableWidth = containerWidth - totalGaps;
            const totalRatio = currentRow.reduce((sum, item) => sum + item.ratio, 0);
            
            // New height = Available Width / Sum of Aspect Ratios
            const newHeight = availableWidth / totalRatio;

            // Apply new height to all images in this row
            currentRow.forEach(item => {
                item.img.style.height = `${newHeight}px`;
                item.img.style.width = 'auto'; // Let browser calculate width
            });

            // Reset for next row
            currentRow = [];
            currentWidth = 0;
        }
    });

    // Handle the last incomplete row (don't stretch it)
    currentRow.forEach(item => {
        item.img.style.height = `${targetHeight}px`;
        item.img.style.width = 'auto';
    });
}
</script>