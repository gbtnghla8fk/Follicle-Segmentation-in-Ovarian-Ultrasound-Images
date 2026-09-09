# LBYEC2B-Final-Project
Image Processing for PCOS Follicles through MATLAB

Used the following to complete the project:

1. Preprocessing and Normalization

   When the image is uploaded, the pipeline converts the image intensity values into floating-point numbers ranging from 0.0 to 1.0. Additionally, border masking is applied to discard the edge artifacts that may be present in the images.
2. Denoising
   
   Anisotropic Diffusion Filtering was used to smooth flat regions while preserving the edges. It uses a gradient threshold to restrict the smoothing across the tissue boundaries and keeps the anatomical details clear. Adaptive tuning automatically calculates the noise variance through the local standard deviation filtering to determine how many diffusion iterations are needed.
3. Region of Interest and Masking
   
   Thresholding isolates the primary tissue region from the background. Functions imclose and imopen fills the small gaps and holes inside the tissue and remove isolated tiny speckles. This is crucial as speckle artifacts are commonly present in medical ultrasound, and this can degrade image quality and produce an interference pattern. The function imfill on the other hand, fills the internal holes to create a solid tissue mask. Spatial cropping is also applied to trim off artifacts on the far-left side of the ultrasound frame
   
4. Advanced Segmentation and Feature Extraction

   The function executeRobustSegmentation is a core pipeline where the follicles are detected through a hybrid approach where both segmentation and morphology is used to reliably identify blobs in the ultrasound image. The Maximally Stable Extremal Regions (MSER) is used to find dark stable regions across different intensity thresholds. Since follicles appear as dark oval cysts in ultrasound scans, MSER identifies potential follicles. Active contour segmentation uses the Chan-Vese model to refine the identified boundaries. While the watershed transformation used to split individual follicles that are touching or clustered together. Geometric and intensity gating were also used to discard objects that fail the physiological thresholds commonly identified in PCOS.
   
5. Visualization
   
   RGB channel Manipulation overlays the detected boundaries onto the grayscale base image for clear visual inspection.

Random photos were selected and used from a publicly available dataset cited below:
A, Indirani (2024). PCOS Dataset. figshare. Dataset. https://doi.org/10.6084/m9.figshare.27682557.v1
