## 🖼️ Table of Contents

- [Usage](#usage)
- [Modules](#modules)
    - [app.py](#app-py)
- [Classes](#classes)
    - [DalleModel](#dallemodel)

## 📖 Usage

```python
from flask import Flask, request, jsonify
from flask_cors import CORS, cross_origin
from dalle_model import DalleModel

app = Flask(__name__)
CORS(app)

dalle_model = DalleModel(ModelSize.MEGA)

@app.route("/dalle", methods=["POST"])
@cross_origin()
def generate_images_api():
    json_data = request.get_json(force=True)
    text_prompt = json_data["text"]
    num_images = json_data["num_images"]
    generated_imgs = dalle_model.generate_images(text_prompt, num_images)

    returned_generated_images = []
    for img in generated_imgs:
        buffered = BytesIO()
        img.save(buffered, format="JPEG")
        img_str = base64.b64encode(buffered.getvalue()).decode("utf-8")
        returned_generated_images.append(img_str)

    print(f"Created {num_images} images from text prompt [{text_prompt}]")

    response = {'generatedImgs': returned_generated_images,
                'generatedImgsFormat': 'JPEG'}
    return jsonify(response)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000, debug=False)
```

## 📦 Modules

### app.py

- Initializes the Flask app and sets up the CORS headers.
- Loads the DalleModel and initializes it with the specified model version.
- Defines the `/dalle` endpoint for generating images from text prompts.

## 👥 Classes

### DalleModel

- Loads the DALL-E model and handles the generation of images from text prompts.
- Provides methods for generating images and saving them to disk.