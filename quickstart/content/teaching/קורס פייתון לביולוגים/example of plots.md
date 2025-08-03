---
lang: "en"
title: "Common Plot Types in Data Visualization"
description: "A quick reference guide showcasing essential plot types used in data analysis and visualization."
omit_header_text: true
paginate: false

---
<style>
/* Reset default browser margins if not already done globally */
html, body {
    margin: 0;
    padding: 0;
}

/* --- Plot Gallery Styling --- */

/* Main container for the entire plot gallery */
.plot-gallery-wrapper {
    width: 100vw; /* Occupy 100% of the viewport width */
    height: auto; /* Height will expand as needed by content */
    padding: 30px 20px; /* Increased top/bottom padding for more vertical breathing room */
    box-sizing: border-box; /* Include padding in the total width */
    display: flex;
    flex-direction: column;
    justify-content: flex-start; /* Align content to the top */
    align-items: center; /* Center content horizontally */
    margin: 0 auto; /* No outside margins, relies on padding for spacing */
    background-color: #fcfcfc; /* A very light, subtle background */
}

/* Page title for the gallery */
.plot-gallery-wrapper h2 {
    font-size: 2.2em; /* Slightly larger, more prominent title */
    color: #2c3e50; /* A darker, professional color */
    margin-bottom: 30px; /* More space below the main title */
    text-align: center;
    width: 100%;
}

/* Internal grid container for all plot items */
.plot-gallery-container {
    display: grid;
    /* Going back to 3 columns to allow for slightly smaller, more numerous images horizontally.
       This often creates a more compact and balanced look for a gallery with multiple items. */
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px; /* Increased gap between individual plots for better separation */
    width: 100%;
    max-width: 1200px; /* Optional: Set a max-width for the grid itself to prevent it from
                         getting too wide on very large screens, keeping content readable. */
    height: auto; /* Allow height to grow as needed */
    box-sizing: border-box;
    font-size: 13px; /* Slightly adjusted base font size for grid items */
}

/* Styling for each individual plot item (title + image(s)) */
.plot-gallery-item {
    text-align: center;
    display: flex;
    flex-direction: column; /* Stack title and images vertically */
    justify-content: space-between; /* Distribute space between title and image(s) */
    align-items: center;
    padding: 10px; /* More padding inside each plot item */
    box-sizing: border-box;
    background-color: #ffffff; /* White background for each plot card */
    border-radius: 8px; /* Rounded corners for the plot card */
    box-shadow: 0 4px 8px rgba(0,0,0,0.08); /* Subtle shadow for depth */
    transition: transform 0.2s ease-in-out; /* Smooth hover effect */
}

.plot-gallery-item:hover {
    transform: translateY(-5px); /* Lift card slightly on hover */
}

/* Image sizing within each plot item */
.plot-gallery-item img {
    max-width: 90%; /* Images take up to 90% width of their grid cell */
    /* DECREASED MAX-HEIGHT: This is where we make images a bit smaller.
       Adjust this value to your liking. */
    max-height: 160px; /* Experiment with values like 150px-180px */
    width: auto; /* Allow width to scale proportionally */
    height: auto; /* Allow height to scale proportionally */
    object-fit: contain; /* Maintain aspect ratio without cropping */
    display: block;
    margin: 8px auto; /* More margin between grouped images */
    border-radius: 4px; /* Slightly rounded image corners */
}

/* Title styling for each plot type */
.plot-gallery-item h3 {
    margin: 0 0 10px 0; /* More space below titles within the card */
    font-size: 1.2em; /* Slightly larger title font size within the card */
    color: #34495e; /* A complementary dark blue for titles */
    text-align: center;
    width: 100%;
    white-space: normal; /* Allow long titles to wrap */
}
</style>

<div class="plot-gallery-wrapper">
    <h2>Common Plot Types</h2>
    <div class="plot-gallery-container">
        <div class="plot-gallery-item">
            <h3>Scatter Plots</h3>
            <img src="/example_of_plots/2_ocupied_cell_proprtion_group.png" alt="Occupied Cell Proportion">
            <img src="/example_of_plots/time_graph.png" alt="Time Series Graph">
        </div>
        <div class="plot-gallery-item">
            <h3>Bar Plot</h3>
            <img src="/example_of_plots/life_stage.png" alt="Life Stage Distribution">
        </div>
        <div class="plot-gallery-item">
            <h3>Pie Chart</h3>
            <img src="/example_of_plots/mamel_abundance.png" alt="Mammal Abundance">
        </div>
        <div class="plot-gallery-item">
            <h3>Heatmaps</h3>
            <img src="/example_of_plots/original_land_use_sim.svg" alt="Original Land Use Simulation">
            <img src="/example_of_plots/diulation.png" alt="Dilution Heatmap">
        </div>
        <div class="plot-gallery-item">
            <h3>3D Animation</h3>
            <img src="/example_of_plots/seapration_plane.gif" alt="3D Separation Plane Animation">
        </div>
    </div>
</div>