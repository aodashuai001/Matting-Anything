# Installation Instructions
## MAM Setup
We use Python 3.9, PyTorch 1.13.1 (CUDA 11.7 build), torchvision 0.14.1, diffusers 0.17.0 for local setup. You may specify the version in the requirements.txt to align with our local setup if you meet any version mismatch issues during the installation process.

### Create a conda environment
  
  ```bash
  conda create --name mam python=3.9 -y
  conda activate mam
  conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
  ```

### Install packages and other dependencies.

  ```bash
  git clone https://github.com/SHI-Labs/Matting-Anything
  cd Matting-Anything

  # Install all dependencies
  pip install -r requirements.txt

  # Install segment-anything
  python -m pip install -e segment-anything

  # Install Grounding DINO
  export BUILD_WITH_CUDA=True
  export CUDA_HOME=/path/to/cuda/
  python -m pip install -e GroundingDINO

  #Install diffusers
  pip install --upgrade diffusers[torch]

  cd .\GroundingDINO\
  pip install -q -e .
  ```
More details can be found in [segment anything](https://github.com/facebookresearch/segment-anything#installation) and [ GroundingDINO](https://github.com/IDEA-Research/GroundingDINO#install) if you meet any installation issues.

### Download the pre-trained weights.

  ```bash
  mkdir checkpoints
  cd checkpoints

  # Download GroundingDINO model
  wget https://github.com/IDEA-Research/GroundingDINO/releases/download/v0.1.0-alpha/groundingdino_swint_ogc.pth

  # Download MAM models
  https://drive.google.com/drive/folders/1Bor2jRE0U-U6PIYaCm6SZY7qu_c1GYfq?usp=sharing
  ```

## Gradio Setup
You can set up the gradio demo locally by simply running 
```bash
python gradio_app.py
```
to launch and play with the demo based on the SAM ViT-B model.
We support 3 prompt types in the local Gradio app for MAM：

1. **scribble_point**: Click a point on the target instance for matting.
2. **scribble_box**: Click on two points, the top-left point and the bottom-right point to represent a bounding box of the target instance.
3. **text**: Send a text prompt to identify the target instance in the `Text Prompt` box.

We support 2 background types to support image composition with the alpha matte output:

1. **real_world_sample**: Randomly select a real-world image from `assets/backgrounds` for composition.
2. **generated_by_text**: Send a background text prompt to create a background image with the stable diffusion model in the `Background Prompt` box.

You can also play with the demo online at [HuggingFace](https://huggingface.co/spaces/shi-labs/Matting-Anything).
