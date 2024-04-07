**Table of Contents**

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Usage](#usage)
  * [API](#api)
    * [`/dalle`](#dalle)
* [Contributing](#contributing)
* [License](#license)

## Overview

This Flask-based API server provides access to the DALL-E generative AI model, allowing users to convert text prompts into images.

## Prerequisites

- Python 3.6+
- Flask
- Pillow
- DALL-E model (available through `dalle_model` package)

## Installation

```bash
pip install -r requirements.txt
```

## Usage

### API

#### `/dalle`

**Request**

```json
{
  "text": "A photo of a cat wearing a top hat",
  "num_images": 1
}
```

**Response**

```json
{
  "generatedImgs": ["base64-encoded-image-data"],
  "generatedImgsFormat": "JPEG"
}
```

## Contributing

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) before submitting a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.