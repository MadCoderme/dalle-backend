**Table of Contents:**

* [Introduction](#introduction)
* [Usage](#usage)
* [Configuration](#configuration)
* [Backend API](#backend-api)

**Introduction**

This document provides a comprehensive overview of the internal DALL-E backend server for the team's use. The server utilizes DALL-E models to generate images from text prompts.

**Usage**

To use the server, send a POST request to the `/dalle` endpoint with a JSON payload containing the following fields:

* `text`: The text prompt to generate images from
* `num_images`: The number of images to generate (max 100)

Example usage:

```python
import requests

data = {
    "text": "A beautiful landscape with mountains and a lake",
    "num_images": 5
}

response = requests.post("http://localhost:8000/dalle", json=data)
```

The response will be a JSON object containing a list of base64-encoded images.

**Configuration**

The server can be configured using the following command-line arguments:

| Argument | Description | Default |
|---|---|---|
| `--port` | The port to run the server on | 8000 |
| `--model_version` | The version of the DALL-E model to use | Mini |
| `--save_to_disk` | Whether to save generated images to disk | False |
| `--img_format` | The format of generated images | JPEG |
| `--output_dir` | The directory to save generated images to | `DEFAULT_IMG_OUTPUT_DIR` |

**Backend API**

The server exposes the following API endpoints:

| Endpoint | Method | Description |
|---|---|---|
| `/` | GET | Returns a welcome message |
| `/dalle` | POST | Generates images from a text prompt |

**Example Usage**

To generate 5 images from the text prompt "A beautiful landscape with mountains and a lake", you can send the following POST request:

```
curl -X POST -H 'Content-Type: application/json' -d '{"text": "A beautiful landscape with mountains and a lake", "num_images": 5}' http://localhost:8000/dalle
```

The response will be a JSON object containing a list of base64-encoded images, which you can then decode and save to disk.