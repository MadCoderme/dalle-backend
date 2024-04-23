**DALL-E Flask App**

**Table of Contents**

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Setup](#setup)
* [Usage](#usage)
* [Command-line Arguments](#command-line-arguments)
* [API Reference](#api-reference)
* [Additional Notes](#additional-notes)

## Overview

This Flask app provides a convenient interface to interact with the DALL-E model, allowing you to generate images from text prompts.

## Prerequisites

- Python 3.8 or later
- Flask
- DALL-E model (see [Setup](#setup) for details)

## Setup

1. Clone this repository.
2. Install the required packages: `pip install -r requirements.txt`.
3. Download the DALL-E model from [HuggingFace](https://huggingface.co/models/dalle-mini).
4. Set the `DALLE_MODEL_PATH` environment variable to point to the downloaded model directory.

## Usage

Start the app using the following command:

```
python app.py
```

By default, the app listens on port 8000.

## Command-line Arguments

The app can be configured using the following command-line arguments:

| Argument | Type | Default | Description |
|---|---|---|---|
| `--port` | int | 8000 | The port to listen on. |
| `--model_version` | string | Mini | The version of the DALL-E model to use (mini, mega, or mega_full). |
| `--save_to_disk` | boolean | False | Whether or not to save the generated images to disk. |
| `--img_format` | string | JPEG | The format of the generated images (JPEG or PNG). |
| `--output_dir` | string | DEFAULT_IMG_OUTPUT_DIR | The directory to save the generated images to. |

## API Reference

### `/dalle` (POST)

**Request body:**

| Field | Type | Description |
|---|---|---|
| text | string | The text prompt to generate images from. |
| num_images | int | The number of images to generate. |

**Response body:**

| Field | Type | Description |
|---|---|---|
| generatedImages | list of strings | Base64-encoded images generated from the prompt. |
| generatedImgsFormat | string | The format of the generated images (JPEG or PNG). |

## Additional Notes

- The app uses the `flask-cors` package to allow cross-origin requests.
- The app is not production-ready and should not be used in a production environment.