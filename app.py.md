## :computer: DALL-E Server with Flask API

### Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
    - [Start the Server](#start-the-server)
    - [Generate Images](#generate-images)
- [API](#api)
    - [/dalle](#dalle)
- [Command-Line Arguments](#command-line-arguments)
- [Additional Notes](#additional-notes)

### Prerequisites

- Python 3.8 or higher
- Flask
- Pillow
- Transformers
- A GPU with at least 4GB of VRAM

### Installation

1. Clone the repository:
```bash
git clone https://github.com/your-username/dalle-server.git
```

2. Install the required packages:
```bash
pip install -r requirements.txt
```

### Usage

**Assuming you have already installed the prerequisites and cloned the repository** 

#### Start the Server

To start the server, run the following command: 

```bash
python app.py
```

The server will start on port 8000. You can change the port by specifying the `--port` argument.

#### Generate Images

To generate images, send a POST request to the `/dalle` endpoint with the following JSON payload:

```json
{
  "text": "Your text prompt",
  "num_images": 4  
}
```

The server will generate the specified number of images and return them as a base64-encoded string.

### API

**POST [dalle]**
- Generates images based on a text prompt and returns them as a base64-encoded string.
- Request Body:
    - `text`: The text prompt to generate images from.
    - `num_images`: The number of images to generate.
- Response Body:
    - `generatedImages`: A list of base64-encoded images.
    - `generatedImgsFormat`: The format of the generated images (e.g. "JPEG", "PNG").

### Command-Line Arguments

The server can be customized using the following command-line arguments:

- `--port`: The port to run the server on.
- `--model_version`: The version of the DALL-E model to use. Can be "mini", "mega", or "mega-full".
- `--save_to_disk`: Whether to save the generated images to disk.
- `--img_format`: The format of the generated images (e.g. "JPEG", "PNG").
- `--output_dir`: The directory to save the generated images to.

### Additional Notes

- The server uses the DALL-E mini model by default. To use the mega or mega-full models, you will need a GPU with at least 10GB of VRAM.
- The server can generate up to 10 images at a time.
- The server is still under development. Please report any bugs or issues on GitHub.