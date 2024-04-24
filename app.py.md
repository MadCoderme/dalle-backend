## 🖼️ DALL-E API 📸

### Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Usage](#usage)
  - [API Endpoints](#api-endpoints)
    - [Hello World Endpoint](#hello-world-endpoint)
    - [DALL-E Generation Endpoint](#dalle-generation-endpoint)
  - [Example Usage Code](#example-usage-code)
- [Configuration](#configuration)
- [Authors](#authors)

### Overview

This API provides a simple and easy-to-use interface to [DALL-E](https://openai.com/dall-e-2/), a powerful AI model that can generate images from text descriptions. With this API, you can quickly and easily create stunning images for a variety of purposes, such as:

- Social media posts
- Blog posts
- Presentations
- Marketing materials

### Installation

To install the DALL-E API, simply run the following command:

```bash
pip install dalle-api
```

### Usage

#### API Endpoints

The DALL-E API provides two main endpoints:

##### Hello World Endpoint

This endpoint simply returns a "Hello, World!" message. It can be used to test that the API is up and running.

**Endpoint:**

```
/
```

**Request:**

```
POST
```

**Response:**

```
{
  "message": "Hello, World!"
}
```

##### DALL-E Generation Endpoint

This endpoint generates images from text descriptions.

**Endpoint:**

```
/dalle
```

**Request:**

```
POST
```

**Body:**

```
{
  "text": "A photo of a cat wearing a cowboy hat",  # Text prompt for image generation
  "num_images": 10  # Number of images to generate
}
```

**Response:**

```
{
  "generatedImages": ["image1.png", "image2.png", ..., "image10.png"],
  "generatedImgsFormat": "png"  # Format of the generated images
}
```

#### Example Usage Code

The following code shows how to use the DALL-E API to generate images from text descriptions:

```python
import requests

# Initialize the API client
api_client = requests.Session()

# Set the API endpoint
api_endpoint = "http://localhost:8000/dalle"

# Set the request body
body = {
  "text": "A photo of a cat wearing a cowboy hat",
  "num_images": 10
}

# Send the request
response = api_client.post(api_endpoint, json=body)

# Get the generated images
generated_images = response.json()["generatedImages"]

# Do something with the generated images...
```

### Configuration

The DALL-E API can be configured with the following environment variables:

| Variable | Description | Default Value |
|---|---|---|
| `DALL_E_MODEL_VERSION` | The version of the DALL-E model to use | `mini` |
| `DALL_E_SAVE_TO_DISK` | Whether to save the generated images to disk | `False` |
| `DALL_E_IMG_FORMAT` | The format of the generated images | `JPEG` |
| `DALL_E_OUTPUT_DIR` | The directory to save the generated images to | `/tmp/dalle-images` |

### Authors

This API was developed by a team of engineers at [AI Company Name](https://www.example.com).