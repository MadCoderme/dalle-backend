## DALL-E Server Documentation 🎨

### Table of Contents

* [Introduction](#introduction)
* [Project Structure](#project-structure)
* [Dependencies](#dependencies)
* [Configuration Options](#configuration-options)
* [API Endpoints](#api-endpoints)
    * [/](#/)
    * [/dalle](#dalle)
* [Code Structure](#code-structure)

### Introduction

This Python code implements a server using the Flask framework that exposes an API for generating images from text prompts using the DALL-E model. 

### Project Structure

The project structure is as follows:

```
├── dalle_model.py
├── utils.py
└── app.py
```

### Dependencies

The project requires the following Python packages:

* **argparse:**  For parsing command-line arguments.
* **base64:** For encoding generated images in base64 format.
* **os:** For working with the file system.
* **pathlib:** For working with file paths.
* **io:** For working with byte streams.
* **time:** For generating timestamps.
* **flask:** For building the web server and API.
* **flask_cors:** For enabling cross-origin requests.
* **consts:** For defining constants used in the project. 

### Configuration Options

The following command-line arguments can be used to configure the server:

| Argument | Type | Default | Description |
|---|---|---|---|
| `--port` | `int` | `8000` | Port on which the server listens. |
| `--model_version` | `ModelSize` | `ModelSize.MINI` | DALL-E model version to use (Mini, Mega, or Mega_full). |
| `--save_to_disk` | `bool` | `False` | Whether to save generated images to disk. |
| `--img_format` | `str` | `JPEG` | Format of generated images (JPEG or PNG). |
| `--output_dir` | `str` | `DEFAULT_IMG_OUTPUT_DIR` | Directory where generated images are saved. |

### API Endpoints

#### /

This endpoint returns a simple "hello world" message.

**Method:** GET

**Response:**

```json
"hello world"
```

#### /dalle

This endpoint generates images from a given text prompt.

**Method:** POST

**Request Body:**

```json
{
  "text": "A cat sitting on a beach",
  "num_images": 3
}
```

**Response:**

```json
{
  "generatedImages": [
    "base64 encoded image string",
    "base64 encoded image string",
    "base64 encoded image string"
  ],
  "generatedImgsFormat": "JPEG"
}
```

**Parameters:**

* `text`: The text prompt to use for generating images.
* `num_images`: The number of images to generate.

**Response:**

The response contains a list of base64 encoded image strings and the format of the generated images.

### Code Structure

```python
import argparse
import base64
import os
from pathlib import Path
from io import BytesIO
import time

from flask import Flask, request, jsonify
from flask_cors import CORS, cross_origin
from consts import DEFAULT_IMG_OUTPUT_DIR
from utils import parse_arg_boolean, parse_arg_dalle_version
from consts import ModelSize

app = Flask(__name__)
CORS(app)
print("--> Starting DALL-E Server")

from dalle_model import DalleModel
dalle_model = None

parser = argparse.ArgumentParser(description="A DALL-E app")
parser.add_argument("--port", type=int, default=8000, help="backend port")
parser.add_argument("--model_version", type=parse_arg_dalle_version, default=ModelSize.MINI, help="Mini, Mega, or Mega_full")
parser.add_argument("--save_to_disk", type=parse_arg_boolean, default=False, help="Should save generated images to disk")
parser.add_argument("--img_format", type=str.lower, default="JPEG", help="Generated images format", choices=['jpeg', 'png'])
parser.add_argument("--output_dir", type=str, default=DEFAULT_IMG_OUTPUT_DIR, help="Customer directory for generated images")
args = parser.parse_args()

@app.route("/", methods=["GET"])
@cross_origin()
def hello_api():
    return 'hello world'

@app.route("/dalle", methods=["POST"])
@cross_origin()
def generate_images_api():
    json_data = request.get_json(force=True)
    text_prompt = json_data["text"]
    num_images = json_data["num_images"]
    generated_imgs = dalle_model.generate_images(text_prompt, num_images)

    returned_generated_images = []
    if args.save_to_disk: 
        dir_name = os.path.join(args.output_dir,f"{time.strftime('%Y-%m-%d_%H-%M-%S')}_{text_prompt}")
        Path(dir_name).mkdir(parents=True, exist_ok=True)
    
    for idx, img in enumerate(generated_imgs):
        if args.save_to_disk: 
          img.save(os.path.join(dir_name, f'{idx}.{args.img_format}'), format=args.img_format)

        buffered = BytesIO()
        img.save(buffered, format=args.img_format)
        img_str = base64.b64encode(buffered.getvalue()).decode("utf-8")
        returned_generated_images.append(img_str)

    print(f"Created {num_images} images from text prompt [{text_prompt}]")
    
    response = {'generatedImages': returned_generated_images,
    'generatedImgsFormat': args.img_format}
    return jsonify(response)
    
with app.app_context():
    dalle_model = DalleModel(args.model_version)
    dalle_model.generate_images("warm-up", 1)
    print("--> DALL-E Server is up and running!")
    print(f"--> Model selected - DALL-E {args.model_version}")


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=args.port, debug=False)
```

**Explanation:**

1. **Imports:** Necessary libraries are imported.
2. **Flask App Initialization:** A Flask app is initialized and CORS is enabled.
3. **Argument Parsing:** Command-line arguments are parsed using `argparse`.
4. **DALL-E Model:** The `dalle_model` is initialized within the app context, using the specified model version.
5. **Warm-up:** The `generate_images` method of the `dalle_model` is called with a "warm-up" prompt to initialize the model.
6. **API Endpoints:**
    * `/`: A simple "hello world" endpoint.
    * `/dalle`: Handles POST requests for image generation.
    * **Image Generation:**
        * The endpoint receives the text prompt and number of images to generate from the request body.
        * It calls the `generate_images` method of the `dalle_model` to generate the images.
        * If `save_to_disk` is enabled, the generated images are saved to a directory named after the prompt and timestamp.
        * The generated images are encoded in base64 and returned as a JSON response.

7. **Server Run:** The Flask app is run on the specified port and host.

This code provides a simple yet functional API for generating images using DALL-E. It demonstrates how to use Flask for building a web server, how to parse command-line arguments, and how to use the DALL-E model for image generation.