## DALL-E Server Documentation

### Table of Contents

- [Introduction](#introduction)
- [Model Configuration](#model-configuration)
- [API Endpoints](#api-endpoints)
- [Usage](#usage)
- [Notes](#notes)

### Introduction

This is a Flask-based DALL-E server that allows users to generate images from text prompts. The server is highly configurable and supports various model sizes, image formats, and output directory options.

### Model Configuration

The server can be configured to use different DALL-E model versions. The available options are:

- `Mini`: The smallest and fastest model, suitable for quick prototyping and experimentation.
- `Mega`: A larger and more powerful model, capable of generating higher-quality images.
- `Mega_full`: The largest and most powerful model, capable of generating the highest-quality images.

The model version can be specified using the `--model_version` command-line argument or by setting the `DALLE_MODEL_VERSION` environment variable.

### API Endpoints

The server exposes two API endpoints:

- `/dalle`: This endpoint generates images from a text prompt. It accepts a JSON payload with the following fields:
    - `text`: The text prompt to generate images from.
    - `num_images`: The number of images to generate.
- `/health_check`: This endpoint returns a simple JSON response indicating whether the server is up and running.

### Usage

To use the server, follow these steps:

1. Install the required Python dependencies using `pip install -r requirements.txt`.
2. Start the server using the following command: `python server.py`.
3. Send a POST request to the `/dalle` endpoint with the desired text prompt and number of images.
4. The server will generate the images and return them as base64-encoded strings in the response.

### Notes

- The server saves generated images to disk if the `--save_to_disk` command-line argument is set to `True`. The images are saved in the directory specified by the `--output_dir` argument.
- The server supports both JPEG and PNG image formats. The format can be specified using the `--img_format` command-line argument.
- The server can be used with any DALL-E model as long as the model is compatible with the `dalle-mini` Python library.