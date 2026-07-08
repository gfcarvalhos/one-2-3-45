# README: One-2-3-45: Single Image to 3D Mesh

This Colab notebook implements the 'One-2-3-45' model to generate 3D meshes from a single image. It configures the environment, installs the required dependencies, downloads the model checkpoints, and runs inference to convert 2D images into 3D models, as well as allowing the visualization of the results.

## Initial Setup

**Runtime Requirements:**

- Runtime: `2025.07`
- GPU: A100 (or compatible with high RAM)

**Steps:**

1. Make sure that the Colab runtime is configured according to the requirements (A100 GPU, high RAM).
2. Run all cells in order. After Cell 2, Colab may ask to restart the runtime — do so and continue from Cell 3.

### Clone Repository

To get started, clone the project repository. If you already have the code in your Google Drive, you can skip this step and adjust the `PROJECT_DIR` in Cell 3.

```bash
!git clone [https://github.com/your_username/One-2-3-45-master.git](https://github.com/your_username/One-2-3-45-master.git)
# Replace 'your_username' with the original repository username or organization, if available.
```

## Notebook Flow

### Cell 1 — Install PyTorch 2.1 + CUDA 12.1

This cell replaces the default PyTorch version in Colab with a specific version (2.1 + CUDA 12.1) that is compatible with the `torchsparse` library used by the project. This ensures that all dependencies work correctly together.

### Cell 2 — Install TorchSparse v1.4.0

Compiles and installs the `TorchSparse` library version 1.4.0 with CUDA support. This is a crucial step for the model's performance. **IMPORTANT:** After running this cell, if requested by Colab, **RESTART THE RUNTIME** (`Runtime > Restart runtime`) before proceeding to Cell 3.

### Cell 3 — Mount Drive and configure project

Mounts your Google Drive into the Colab environment to access files and save results. You will need to **ADJUST THE FOLDER PATH (`PROJECT_DIR`)** to where the 'One-2-3-45-master' repository is located in your Drive. The cell also verifies the PyTorch version, CUDA version, and the GPU currently in use.

### Cell 4 — Install Python dependencies

Installs all additional Python libraries required for the project, such as `albumentations`, `opencv-python`, `pytorch-lightning`, `diffusers`, `CLIP`, `segment-anything`, among others. It also includes a patch to ensure compatibility with the PyTorch and NumPy versions.

### Cell 5 — Download Checkpoints (first time only)

This cell handles the download of the model checkpoints required for inference. The files are saved to your Google Drive (around 10 GB). The script checks if the checkpoints already exist and only downloads the missing ones, saving time and bandwidth.

### Cell 6 — Run Inference

Executes the inference process to generate a 3D mesh from an example image (`./demo/demo_examples/01_wild_hydrant.png`). The estimated processing time is approximately 2-3 minutes on an A100 GPU. The output is a `.ply` file (3D mesh).

### Cell 7 — Use your own image

Allows you to process your own images located in the `./inputs/edited/` folder. The cell iterates over all images found in that folder and runs the 3D inference for each one, generating their respective meshes. If you want to use an image from another location in your Drive, use **Option B** in cell `a4pbp5xPwsiQ` by uncommenting and adjusting the path.

### Cell 8 — Visualize results

This section contains two cells to visualize the results:

- **3D Mesh Visualization (`qbJY06U_BBqv`):** Loads and displays the generated `.ply` files using `plotly.graph_objects.Mesh3d`, allowing an interactive inspection of the 3D models.
- **Views Visualization (`Yel9KzgiwsiQ`):** Displays the different 2D views generated during the inference process, which are used to construct the 3D model. This helps to understand how the model "sees" the object before the final reconstruction.

### Final Cell — Copy Meshes to Output Folder

This cell collects all the `mesh.ply` files generated within the experiment folders (`./exp/`) and copies them to a centralized `./outputs/` folder. This facilitates access and organization for all the 3D models resulting from the processing.
