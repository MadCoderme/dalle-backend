## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
    - [API](#api)
    - [Health Check](#health-check)
- [Configuration](#configuration)
- [Demo](#demo)
- [Contributing](#contributing)

## Introduction

This project provides a user-friendly interface to access the DALL-E 2 model. With a simple API call, users can generate high-quality images from text prompts.

## Installation

To install the required dependencies, run the following command:

```
pip install -r requirements.txt
```

## Usage

### API

To generate images using the API, send a POST request to the `/dalle` endpoint with the following JSON body:

```
{
  "text": "Your text prompt",
  "num_images": "Number of images to generate"
}
```

The API will return a JSON response with the generated images encoded as base64 strings.

### Health Check

To check the health of the server, send a GET request to the `/` endpoint. The server will return a JSON response with a `success` field set to `True`.

## Configuration

The following command-line arguments can be used to configure the server:

- `--port`: The port on which the server will listen (default: 8000)
- `--model_version`: The version of the DALL-E model to use (default: "mini")
- `--save_to_disk`: Whether to save the generated images to disk (default: False)
- `--img_format`: The format of the generated images (default: "JPEG")
- `--output_dir`: The directory in which to save the generated images (default: "./output")

## Demo

A live demo of the server is available at [https://dalle-server.herokuapp.com/](https://dalle-server.herokuapp.com/).

## Contributing

Contributions are welcome! Please read the [contributing guidelines](https://github.com/username/project-name/blob/main/CONTRIBUTING.md) before submitting a pull request.

## License

This project is licensed under the MIT License.