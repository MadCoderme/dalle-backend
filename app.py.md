## **Internal Documentation for DALL-E Server**

### **About**

This Flask API enables users to generate images from text prompts using the DALL-E model. It features a user-friendly interface and robust functionality.

### **Usage**

To run the server, execute the following command:

```
$ python app.py
```

### **API**

The API comprises the following endpoints:

#### `/`

**Method:** GET

**Description:** Returns a greeting message.

#### `/dalle`

**Method:** POST

**Description:** Generates images from a provided text prompt.

**Request Body:**

- `text`: The text prompt for image generation.
- `num_images`: The desired number of generated images.

**Response:**

- `generatedImages`: A list of base64-encoded generated images.
- `generatedImgsFormat`: The format of the generated images.

### **Code Structure**

#### **app.py**

- Defines the Flask app.
- Configures CORS for cross-origin requests.
- Parses command-line arguments.
- Initializes the DALL-E model.
- Defines API routes.

#### **dalle_model.py**

- Encapsulates the logic for generating images using the DALL-E model.

#### **utils.py**

- Provides helper functions for argument parsing and text prompt tokenization.

#### **consts.py**

- Stores constants, such as the default output directory and available DALL-E model sizes.

### **Arguments**

| Argument | Description |
|---|---|
| `--port` | Port for the API to run on. |
| `--model_version` | Version of the DALL-E model (Mini, Mega, Mega_full). |
| `--save_to_disk` | Enables saving generated images to disk. |
| `--img_format` | Format of generated images (JPEG, PNG). |
| `--output_dir` | Custom directory for saving generated images. |

### **Constants**

| Constant | Description |
|---|---|
| `DEFAULT_IMG_OUTPUT_DIR` | Default directory for generated images. |
| `ModelSize` | Enumeration of available DALL-E model sizes. |

### **Requirements**

- Python 3.6+
- Flask
- Flask-CORS
- DALL-E model
- Base64
- io
- pathlib
- argparse