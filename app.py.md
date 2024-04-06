### 📖 DALL-E Server App

**Table of Contents**

- [Overview](#overview)
- [Usage](#usage)
    - [API](#api)
    - [CLI](#cli)
- [Requirements](#requirements)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Known Issues](#known-issues)

---

## 📝 Overview

This app is a REST API that uses the DALL-E model to generate images from text prompts. 
This can be used for a variety of purposes, such as generating new ideas for creative projects or creating visual assets for marketing and advertising.

---

## 🛠 Usage

### API

The API is a simple POST endpoint that takes a JSON payload with the following format:

```json
{
  "text": "Your text prompt",
  "num_images": 1
}
```

The output will be a JSON response with the following format:

```json
{
  "generatedImgs": ["base64 encoded images"]
}
```

### CLI

To use the CLI, simply run the following command:

```bash
python dalle_server.py --text "Your text prompt" --num_images 1
```

---

## 📋 Requirements

The following software is required to run this app:

- Python 3.8 or later
- Flask
- Flask-CORS
- DALL-E model

---

## ⚙️ Configuration

The following configuration options are available:

| Option | Description | Default |
|---|---|---|
| port | The port to run the app on | 8000 |
| model_version | The version of the DALL-E model to use | "mini" |
| save_to_disk | Whether to save the generated images to disk | False |
| img_format | The format of the generated images | "JPEG" |
| output_dir | The directory to save the generated images to | "./output" |

---

## 🚀 Deployment

To deploy this app, simply run the following command:

```bash
gunicorn --bind 0.0.0.0:8000 dalle_server:app
```

---

## ⚠️ Known Issues

There are no known issues with this app at this time.

---

## 💻 Example Usage

```python
import requests

# Set the API endpoint and your prompt
api_endpoint = "http://localhost:8000/dalle"
prompt = "A majestic painting of a cat wearing a crown"

# Send the request to the API
data = {"text": prompt, "num_images": 1}
response = requests.post(api_endpoint, json=data)

# Get the generated image
generated_image = response.json()["generatedImgs"][0]

# Save the image to disk
with open("generated_image.jpg", "wb") as f:
    f.write(base64.b64decode(generated_image))
```