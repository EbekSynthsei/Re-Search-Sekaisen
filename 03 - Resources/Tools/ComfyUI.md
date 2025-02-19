---
cssclasses: 
tags:
  - guides
  - "#IA"
  - "#python"
  - "#unity"
  - "#blender"
  - done
date: 2025-02-19T15:05:00
---
# Resources

[ComfyUI Repo](https://github.com/comfyanonymous/ComfyUI.git)
[Stable Diffusion Animation Repo](https://github.com/tobias17/sd-pixel-anims.git)

---
## MODELS:

Scaricare il modello consigliato e porlo sotto la cartella models/checkpoints.
L' installazione dei modelli può essere fatta ed è consigliata tramite il Comfyui manager.

[Stable diffusion 1.5](https://huggingface.co/Comfy-Org/stable-diffusion-v1-5-archive/blob/main/v1-5-pruned-emaonly-fp16.safetensors)

[Juggernaut XL](https://civitai.com/models/133005/juggernaut-xl) 

[PixelArtLoRa](https://civitai.com/models/120096/pix...)

[OpenPoseXL](https://huggingface.co/thibaud/controlnet-openpose-sdxl-1.0/blob/main/OpenPoseXL2.safetensors)

[TripoSR](https://huggingface.co/spaces/stabilityai/stable-fast-3d) 

## RECOMMENDED WAY TO UPDATE:
To update the ComfyUI code: update\update_comfyui.bat

---
# Install ComfyUI Manager

[ComfyUI Manager Repo](https://github.com/ltdrdata/ComfyUI-Manager.git)

E' un singolo file bat da porre nella cartella di installazione e lanciare (due semplici comandi pip install Python è necessario e consigliato nella versione 3.12 - io ho la 3.13)

Open ComfyUI and drop those files.
If missing models check the installations and redo via manager.

---

# Usage:

### Step 1: Create a T-POSE model of the desired image via ComfyUI.

- Think of a desired model and write down a simple description of the humanoid you desire to model
- Head over to ollama or fabric to get a nice prompt and a list of the desired materials (or the ones to exclude).
- Go to ComfyUI (is a self contained folder in Desktop now) and run **run_nvidia_gpu.bat**
- Paste the description and the materials listed
- Run the generation
- Save the resulting png

---

### Step 2:  Generate a 3D model via TRIPO-SR

- Head over to the space of Tripo-SR
- Download the resulting OBJ file

---

### Step 3: Modify model in Blender

* Create a folder for your workspace
* Import OBJ file into Blender (delete default cube first)
* Head over to shading
* Select the carachter
* Search for color attribute node and drag into base color
* Roughness should be around 0.85
* Save the workspace
* Export as a .fbx files in the path node
* Switch the path mode from auto to copy
* Limit to selected only and uncheck animation

---

### Step 4: Prepare animations in Mixamo

* Upload to mixamo the model
* Put the rigs
* Get the autorigging done
* Choose an animation via the search bar
* Check the in place animation box
* Check the download options
* Continue for as many animations are needed

---

### Step 5: Import the animations in Blender and render

* Import an FBX file.
* Remember to add the color node to the shading menu
* Go back to the layout and set up camera and lights.
* Check the Resolution of the images (multiple of 8).
* Delete the default camera and set the camera to the chosen one
* The animation from mixamo don't start from zero but from one
* Get the animation to loop properly
* World properties settings maybe not fitted so adjust lighting for a nice background
* Render animation
* You now have the animation images

---

### Step 6: Cleanup the animation images

- In ComfyUI choose the pixelate folder workflow
- Choose the folder to pixelate
- Check the preview and adjust parameters
- Grab the outputs and paste them into the correct folder
- Run via cmd the rembg python script.
- Cleanup the shenanigans via other tools [[PIXEL STUDIO]]/[[ASEPRITE]]
- Compress the images in spritesheets useful for Game Engines like [[Unity]] via the compress script.

---

# References:

[Pixel Art Made By AI](https://youtu.be/MUr1iRdMywo?si=x3FMdZsYKPUjz6cw)
