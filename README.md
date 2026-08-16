# Text-to-Image and Text-to-Video Generation

The core research problem: general-purpose text-to-image/video models (e.g. SDXL) translate text into images using surface-level token association, which fails on content requiring cultural context, metaphor, and abstract concept resolution. This project solves that problem with a document-enhanced ontological reasoning layer sitting between raw text and the diffusion model, combined with automated hyperparameter tuning and stochasticity control to make diffusion output reliable enough for a production API.

# Key Features
# LLM-based Semantic Decomposition
Converts unstructured input text into a sequence of coherent, visually filmable scenes with consistent characters/subjects across scenes, using a two-stage LLM prompting pipeline (hypothetical document generation → ontological/feature extraction).


# Ontological Prompt Engineering
A structured Subject–Action / Scene–Setting / Time–Weather / Mood–Atmosphere hierarchy that disambiguates abstract concepts before they are ever sent to the image model, then dynamically compresses back into token-efficient prompts (mitigating the CLIP 77-token limit).

# Character & Style Consistency
Explicit re-description strategy per scene (since diffusion models have no memory of "the same person") to preserve subject identity across a multi-scene video.

# Bayesian-Optimized Guidance Scale 
Gaussian-Process-based Bayesian Optimization (with grid-search fallback) automatically tunes SDXL's classifier-free guidance scale per generation task by maximizing CLIP image–text similarity, rather than relying on a fixed default.

# Stochasticity Control via Multi-Sampling
Generates n candidate images per scene and selects the best by CLIP score, reducing the variance inherent to diffusion sampling.

# Two-Stage SDXL Base+Refiner Pipeline 
High-resolution (1024×1024) image synthesis with a dedicated refiner pass for detail enhancement.

# Image-to-Video Animation
Combines Stable Video Diffusion (temporal motion synthesis) with an SDXL Img2Img sliding-window interpolation technique to generate smooth cross-scene transitions, subtitle overlay, and a final exportable MP4.

# Asynchronous REST API
Flask-based server with background task processing, real-time progress polling, and file download endpoints — built for direct consumption by a mobile client over an ngrok public tunnel.


