## Internal Documentation for DALL-E Server Code

### Overview

This document provides an overview of the codebase for the DALL-E server, a web service that allows users to generate images from text prompts using the DALL-E model. The code is organized into several modules and utilizes various libraries and frameworks.

### Code Structure

The codebase is structured as follows:

- `consts.py`: Defines constants used throughout the code, such as the default output directory for generated images.
- `utils.py`: Contains helper functions for parsing arguments and converting data types.
- `dalle_model.py`: Encapsulates the DALL-E model and provides methods for generating images.
- `app.py`: Defines the Flask application and handles API requests for image generation.

### Flask Application

The Flask application is configured with CORS enabled to allow cross-origin requests. It defines two endpoints:

- `/`: Returns a simple "hello world" message.
- `/dalle`: Handles image generation requests. This endpoint accepts a JSON payload containing the text prompt and the number of images to generate.

### DALL-E Model Initialization

The DALL-E model is initialized within the application context using the specified model version. Before serving requests, the model generates a single image as a warm-up to ensure readiness.

### Image Generation and Output

The image generation process is handled by the `dalle_model` module. Generated images are returned as base64-encoded strings within a JSON response. Additionally, if the `--save_to_disk` option is enabled, images are saved to the specified output directory with unique filenames.

### Command-Line Arguments

The code supports several command-line arguments for customization:

- `--port`: Backend port number (default: 8000)
- `--model_version`: DALL-E model size (default: Mini)
- `--save_to_disk`: Enable saving generated images to disk
- `--img_format`: Format of generated images (default: JPEG)
- `--output_dir`: Custom output directory for saved images

### Execution

To run the DALL-E server, execute the following command from the project root directory:

```
python app.py
```

This will start the server and make it accessible at the specified port.