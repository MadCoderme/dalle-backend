## Table of Contents

- [About](#about)
- [Usage](#usage)
- [API](#api)
    - [/](#/)
    - [/dalle](#/dalle)
- [Code Structure](#code-structure)
    - [app.py](#app.py)
    - [dalle_model.py](#dalle_model.py)
    - [utils.py](#utils.py)
    - [consts.py](#consts.py)
- [Arguments](#arguments)
- [Constants](#constants)
- [Requirements](#requirements)

## About

This Flask API allows users to generate images from text prompts using the DALL-E model.

## Usage

```
$ python app.py
```

## API

### /

- **Method:** GET
- **Description:** A simple endpoint that returns a greeting message.

### /dalle

- **Method:** POST
- **Description:** Generates images from a given text prompt.
- **Request Body:**
    - `text`: The text prompt to use for image generation.
    - `num_images`: The number of images to generate.
- **Response:**
    - `generatedImages`: A list of base64-encoded images.
    - `generatedImgsFormat`: The format of the generated images.

## Code Structure

### app.py

- **Flask App:** The main Flask app is defined here.
- **CORS Configuration:** CORS is configured to allow cross-origin requests.
- **Argument Parsing:** Command-line arguments are parsed using the `argparse` library.
- **DALL-E Model Initialization:** An instance of the `DalleModel` class is created.
- **API Routes:** The `/` and `/dalle` API routes are defined.

### dalle_model.py

- **DalleModel Class:** This class encapsulates the logic for generating images using the DALL-E model.

### utils.py

- **Helper Functions:** This module contains helper functions for parsing command-line arguments and converting text prompts to tokens.

### consts.py

- **Constants:** This module contains constants used throughout the application, such as the default output directory for generated images and the available DALL-E model sizes.

## Arguments

| Argument | Description |
|---|---|
| `--port` | The port on which the API will run. |
| `--model_version` | The version of the DALL-E model to use. |
| `--save_to_disk` | Whether to save the generated images to disk. |
| `--img_format` | The format of the generated images. |
| `--output_dir` | The customer directory for generated images. |

## Constants

| Constant | Description |
|---|---|
| `DEFAULT_IMG_OUTPUT_DIR` | The default directory for generated images. |
| `ModelSize` | An enumeration of the available DALL-E model sizes. |

## Requirements

- Python 3.6+
- Flask
- Flask-CORS
- DALL-E model
- Base64
- io
- pathlib
- argparse