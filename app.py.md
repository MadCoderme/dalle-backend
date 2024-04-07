**DALL-E Flask App**

**Table of Contents**

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Setup](#setup)
* [Usage](#usage)
* [API Reference](#api-reference)
* [Example Usage](#example-usage)

## Overview

This Flask app provides a convenient interface to interact with the DALL-E model, allowing you to generate images from text prompts.

## Prerequisites

- Python 3.8 or later
- Flask
- DALL-E model (see [Setup](#setup) for details)

## Setup

- Clone this repository.
- Install the required packages: `pip install -r requirements.txt`.
- Download the DALL-E model from [HuggingFace](https://huggingface.co/models/dalle-mini).
- Set the `DALLE_MODEL_PATH` environment variable to point to the downloaded model directory.

## Usage

Start the app using the following command:

```
python app.py
```

By default, the app listens on port 8000.

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
| generatedImgs | list of strings | Base64-encoded images generated from the prompt. |
| generatedImgsFormat | string | The format of the generated images (JPEG or PNG). |

## Example Usage

```python
import requests

# Set the URL and headers for the API call
url = 'http://localhost:8000/dalle'
headers = {'Content-Type': 'application/json'}

# Prepare the JSON payload
payload = {
    'text': 'A photo of a cat wearing a cowboy hat',
    'num_images': 1
}

# Send the API request
response = requests.post(url, json=payload, headers=headers)

# Parse the response
data = response.json()

# Decode and display the generated image
image = base64.b64decode(data['generatedImgs'][0])
with open('generated_image.jpg', 'wb') as f:
    f.write(image)
```

## Additional Notes

- The app can be configured using the following command-line arguments:
    - `--port`: The port to listen on.
    - `--model_version`: The version of the DALL-E model to use (mini, mega, or mega_full).
    - `--save_to_disk`: Whether or not to save the generated images to disk.
    - `--img_format`: The format of the generated images (JPEG or PNG).
    - `--output_dir`: The directory to save the generated images to.
- The app uses the `flask-cors` package to allow cross-origin requests.
- The app is tested using Pytest.