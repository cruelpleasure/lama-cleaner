<h1 align="center">Lama Cleaner</h1>
<p align="center">A free and open-source inpainting tool powered by SOTA AI model.</p>

<p align="center">
  <a href="https://github.com/Sanster/lama-cleaner">
    <img alt="total download" src="https://pepy.tech/badge/lama-cleaner" />
  </a>
  <a href="https://pypi.org/project/lama-cleaner/">
    <img alt="version" src="https://img.shields.io/pypi/v/lama-cleaner" />
  </a>
  <a href="https://colab.research.google.com/drive/1e3ZkAJxvkK3uzaTGu91N9TvI_Mahs0Wb?usp=sharing">
    <img alt="Open in Colab" src="https://colab.research.google.com/assets/colab-badge.svg" />
  </a>

  <a href="https://huggingface.co/spaces/Sanster/Lama-Cleaner-lama">
    <img alt="Hugging Face Spaces" src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue" />
  </a>

  <a href="">
    <img alt="python version" src="https://img.shields.io/pypi/pyversions/lama-cleaner" />
  </a>
  <a href="https://hub.docker.com/r/cwq1913/lama-cleaner">
    <img alt="version" src="https://img.shields.io/docker/pulls/cwq1913/lama-cleaner" />
  </a>
</p>

https://user-images.githubusercontent.com/3998421/196976498-ba1ad3ab-fa18-4c55-965f-5c6683141375.mp4

## Features

- Completely free and open-source
- Fully self-hosted
- [Windows 1-Click Installer](./scripts/README.md)
- Classical image inpainting algorithm powered by [cv2](https://docs.opencv.org/3.4/df/d3d/tutorial_py_inpainting.html)
- Multiple SOTA AI models
    1. [LaMa](https://github.com/saic-mdal/lama)
    2. [LDM](https://github.com/CompVis/latent-diffusion)
    3. [ZITS](https://github.com/DQiaole/ZITS_inpainting)
    4. [MAT](https://github.com/fenglinglwb/MAT)
    5. [FcF](https://github.com/SHI-Labs/FcF-Inpainting)
    6. [SD1.5/SD2](https://github.com/runwayml/stable-diffusion)
    7. [Manga](https://github.com/msxie92/MangaInpainting)
    8. [Paint by Example](https://github.com/Fantasy-Studio/Paint-by-Example)
- Support CPU & GPU
- Various inpainting [strategy](#inpainting-strategy)
- Run as a desktop APP
- [Interactive Segmentation](https://github.com/Sanster/lama-cleaner/releases/tag/0.28.0) on any object

## Usage

A great introductory [youtube video](https://www.youtube.com/watch?v=aYia7Jvbjno&ab_channel=Aitrepreneur) made by **Aitrepreneur**

<details>
<summary>1. Remove any unwanted things on the image</summary>

| Usage                         | Before                                        | After                                               |
|-------------------------------|-----------------------------------------------|-----------------------------------------------------|
| Remove unwanted things        | ![unwant_object2](./assets/unwant_object.jpg) | ![unwant_object2](./assets/unwant_object_clean.jpg) |
| Remove unwanted person        | ![unwant_person](./assets/unwant_person.jpg)  | ![unwant_person](./assets/unwant_person_clean.jpg)  |
| Remove text                   | ![text](./assets/unwant_text.jpg)             | ![text](./assets/unwant_text_clean.jpg)             |
| Remove watermark              | ![watermark](./assets/watermark.jpg)          | ![watermark_clean](./assets/watermark_cleanup.jpg)  |
| Remove text balloons on manga | ![manga](./assets/manga.png)                  | ![manga_clean](./assets/manga_clean.png)            |

</details>

<details>
<summary>2. Fix old photo</summary>

| Usage         | Before                              | After                                           |
| ------------- | ----------------------------------- | ----------------------------------------------- |
| Fix old photo | ![oldphoto](./assets/old_photo.jpg) | ![oldphoto_clean](./assets/old_photo_clean.jpg) |

</details>

<details>
<summary>3. Replace something on the image </summary>

SD1.5/SD2

| Usage                  | Before                   | After                                                          |
| ---------------------- | ------------------------ | -------------------------------------------------------------- |
| Text Driven Inpainting | ![dog](./assets/dog.jpg) | Prompt: a fox sitting on a bench<br/> ![fox](./assets/fox.jpg) |


Paint by Example

| Original Image | Example Image | Result Image |
|----|------|-------|
|<img src="https://user-images.githubusercontent.com/3998421/206908542-c6465ca3-6414-4593-8318-0c8b569e7682.jpg">|[<img src="https://user-images.githubusercontent.com/3998421/206908517-bd7f62d2-464a-43bc-892e-dbea45f7b104.jpeg">](https://youtu.be/NSAN3TzfhaI)|[<img src="https://user-images.githubusercontent.com/3998421/206903752-0463a0cf-146d-4125-a969-8fe20127a09b.jpeg">](https://youtu.be/NSAN3TzfhaI)|

</details>

## Quick Start

The easiest way to use Lama Cleaner is to install it using `pip`:

```bash
pip install lama-cleaner

# Models will be downloaded at first time used
lama-cleaner --model=lama --device=cpu --port=8080
# Lama Cleaner is now running at http://localhost:8080
```

For stable-diffusion 1.5 model, you need
to [accepting the terms to access](https://huggingface.co/runwayml/stable-diffusion-inpainting), and
get an access token from here [huggingface access token](https://huggingface.co/docs/hub/security-tokens)

If you prefer to use docker, you can check out [docker](#docker)

If you hava no idea what is docker or pip, please check [One Click Installer](./scripts/README.md)

Available command line arguments:

| Name                 | Description                                                                                                         | Default  |
| -------------------- |---------------------------------------------------------------------------------------------------------------------| -------- |
| --model              | lama/ldm/zits/mat/fcf/sd1.5/manga/sd2/paint_by_example See details in [Inpaint Model](#inpainting-model)                                 | lama     |
| --hf_access_token    | stable-diffusion need [huggingface access token](https://huggingface.co/docs/hub/security-tokens) to download model |          |
| --sd-run-local       | Once the model as downloaded, you can pass this arg and remove `--hf_access_token`                                  |          |
| --sd-disable-nsfw    | Disable stable-diffusion NSFW checker.                                                                              |          |
| --sd-cpu-textencoder | Always run stable-diffusion TextEncoder model on CPU.                                                               |          |
| --sd-enable-xformers | Enable xFormers optimizations. See: [facebookresearch/xformers](https://github.com/facebookresearch/xformers)       |          |
| --device             | cuda / cpu / mps                                                                                                         | cuda     |
| --port               | Port for backend flask web server                                                                                   | 8080     |
| --gui                | Launch lama-cleaner as a desktop application                                                                        |          |
| --gui_size           | Set the window size for the application                                                                             | 1200 900 |
| --input              | Path to image you want to load by default                                                                           | None     |
| --debug              | Enable debug mode for flask web server                                                                              |          |

## Inpainting Model

| Model | Description                                                                                                                                                                                                            | Config                                                                                                                                                                                                                                                                            |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cv2   | :+1: No GPU is required, and for simple backgrounds, the results may even be better than AI models.                                                                                                                    |                                                                                                                                                                                                                                                                                   |
| LaMa  | :+1: Generalizes well on high resolutions(~2k)<br/>                                                                                                                                                                    |                                                                                                                                                                                                                                                                                   |
| LDM   | :+1: Possible to get better and more detail result <br/> :+1: The balance of time and quality can be achieved by adjusting `steps` <br/> :neutral_face: Slower than GAN model<br/> :neutral_face: Need more GPU memory | `Steps`: You can get better result with large steps, but it will be more time-consuming <br/> `Sampler`: ddim or [plms](https://arxiv.org/abs/2202.09778). In general plms can get [better results](https://github.com/Sanster/lama-cleaner/releases/tag/0.13.0) with fewer steps |
| ZITS  | :+1: Better holistic structures compared with previous methods <br/> :neutral_face: Wireframe module is **very** slow on CPU                                                                                           | `Wireframe`: Enable edge and line detect                                                                                                                                                                                                                                          |
| MAT   | TODO                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                   |
| FcF   | :+1: Better structure and texture generation <br/> :neutral_face: Only support fixed size (512x512) input                                                                                                              |                                                                                                                                                                                                                                                                                   |
| SD1.5 | :+1: SOTA text-to-image diffusion model                                                                                                                                                                                |                                                                                                                                                                                                                                                                                   |

<details>
<summary> See model comparison detail</summary>

**LaMa vs LDM**

| Original Image                                                                                                                            | LaMa                                                                                                                                                   | LDM                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![photo-1583445095369-9c651e7e5d34](https://user-images.githubusercontent.com/3998421/156923525-d6afdec3-7b98-403f-ad20-88ebc6eb8d6d.jpg) | ![photo-1583445095369-9c651e7e5d34_cleanup_lama](https://user-images.githubusercontent.com/3998421/156923620-a40cc066-fd4a-4d85-a29f-6458711d1247.png) | ![photo-1583445095369-9c651e7e5d34_cleanup_ldm](https://user-images.githubusercontent.com/3998421/156923652-0d06c8c8-33ad-4a42-a717-9c99f3268933.png) |

**LaMa vs ZITS**

| Original Image                                                                                                         | ZITS                                                                                                                       | LaMa                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| ![zits_original](https://user-images.githubusercontent.com/3998421/180464918-eb13ebfb-8718-461c-9e8b-7f6d8bb7a84f.png) | ![zits_compare_zits](https://user-images.githubusercontent.com/3998421/180464914-4db722c9-047f-48fe-9bb4-916ba09eb5c6.png) | ![zits_compare_lama](https://user-images.githubusercontent.com/3998421/180464903-ffb5f770-4372-4488-ba76-4b4a8c3323f5.png) |

Image is from [ZITS](https://github.com/DQiaole/ZITS_inpainting) paper. I didn't find a good example to show the
advantages of ZITS and let me know if you have a good example. There can also be possible problems with my code, if you
find them, please let me know too!

**LaMa vs FcF**

| Original Image                                                                                                    | LaMa                                                                                                                   | FcF                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| ![texture](https://user-images.githubusercontent.com/3998421/188305027-a4260545-c24e-4df7-9739-ac5dc3cae879.jpeg) | ![texture_lama](https://user-images.githubusercontent.com/3998421/188305024-2064ed3e-5af4-4843-ac10-7f9da71e15f8.jpeg) | ![texture_fcf](https://user-images.githubusercontent.com/3998421/188305006-a08d2896-a65f-43d5-b9a5-ef62c3129f0c.jpeg) |

**LaMa vs Manga**

Manga model works better on high-quality manga image then LaMa model.

Original Image
![manga](./assets/manga.png)

| Model |  1080x740  |  1470x1010 |
|--------|------------|------------|
|Manga|![manga_1080x740](https://user-images.githubusercontent.com/3998421/202676629-54f40f20-c55b-4e6d-bcc7-0a4e81fbb27d.png)|![manga_1470x1010](https://user-images.githubusercontent.com/3998421/202675839-4f8012d5-1c10-47ea-9628-20512e86f192.png)|
|[LaMa](https://github.com/saic-mdal/lama)|![lama_1080x740](https://user-images.githubusercontent.com/3998421/202675704-53fa7a3d-ec74-4044-a19c-c673d74bdd28.png)|![lama_1470x1010](https://user-images.githubusercontent.com/3998421/202675746-1e642367-f5d0-4b48-aa8b-5d82f2e29082.png)|

</details>

## Inpainting Strategy

Lama Cleaner provides three ways to run inpainting model on images, you can change it in the settings dialog.

| Strategy     | Description                                                                                            | VRAM   | Speed             |
| ------------ | ------------------------------------------------------------------------------------------------------ | ------ | ----------------- |
| **Original** | Use the resolution of the original image                                                               | High   | :zap:             |
| **Resize**   | Resize the image to a smaller size before inpainting. The area outside the mask will not loss quality. | Midium | :zap: :zap:       |
| **Crop**     | Crop masking area from the original image to do inpainting                                             | Low    | :zap: :zap: :zap: |

## Download Model Manually

If you have problems downloading the model automatically when lama-cleaner start,
you can download it manually. By default lama-cleaner will load model from `TORCH_HOME=~/.cache/torch/hub/checkpoints/`,
you can set `TORCH_HOME` to other folder and put the models there.

- GitHub:
    - [LaMa](https://github.com/Sanster/models/releases/tag/add_big_lama)
    - [LDM](https://github.com/Sanster/models/releases/tag/add_ldm)
    - [ZITS](https://github.com/Sanster/models/releases/tag/add_zits)
    - [MAT](https://github.com/Sanster/models/releases/tag/add_mat)
    - [FcF](https://github.com/Sanster/models/releases/tag/add_fcf)
- Baidu:
    - https://pan.baidu.com/s/1vUd3BVqIpK6e8N_EA_ZJfw
    - passward: flsu

## Development

Only needed if you plan to modify the frontend and recompile yourself.

### Frontend

Frontend code are modified from [cleanup.pictures](https://github.com/initml/cleanup.pictures), You can experience their
great online services [here](https://cleanup.pictures/).

- Install dependencies:`cd lama_cleaner/app/ && yarn`
- Start development server: `yarn start`
- Build: `yarn build`

## Docker

You can use [pre-build docker image](https://github.com/Sanster/lama-cleaner#run-docker-cpu) to run Lama Cleaner. The
model will be downloaded to the cache directory when first time used.
You can mount existing cache directory to start the container,
so you don't have to download the model every time you start the container.

The cache directories for different models correspond as follows:

- lama/ldm/zits/mat/fcf: /root/.cache/torch
- sd1.5: /root/.cache/huggingface

### Run Docker (cpu)

```
docker run -p 8080:8080 \
-v /path/to/torch_cache:/root/.cache/torch \
-v /path/to/huggingface_cache:/root/.cache/huggingface \
--rm cwq1913/lama-cleaner:cpu-0.26.1 \
lama-cleaner --device=cpu --port=8080 --host=0.0.0.0
```

### Run Docker (gpu)

- cuda11.6
- pytorch1.12.1
- minimum nvidia driver 510.39.01+

```
docker run --gpus all -p 8080:8080 \
-v /path/to/torch_cache:/root/.cache/torch \
-v /path/to/huggingface_cache:/root/.cache/huggingface \
--rm cwq1913/lama-cleaner:gpu-0.26.1 \
lama-cleaner --device=cuda --port=8080 --host=0.0.0.0
```

Then open [http://localhost:8080](http://localhost:8080)

### Build Docker image

cpu only

```
docker build -f --build-arg version=0.x.0 ./docker/CPUDockerfile -t lamacleaner .
```

gpu & cpu

```
docker build -f --build-arg version=0.x.0 ./docker/GPUDockerfile -t lamacleaner .
```
