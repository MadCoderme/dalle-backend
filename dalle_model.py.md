## Dalle-Mini Model Interface for Image Generation
### Table of Contents
- [Introduction](#introduction)
- [Loading the Model](#loading-the-model)
- [Tokenizing the Prompt](#tokenizing-the-prompt)
- [Generating Images](#generating-images)
- [Decoding Images](#decoding-images)
- [Example Usage](#example-usage)

### Introduction
This documentation provides a comprehensive guide to using the Dalle-Mini model interface for image generation. The interface simplifies the process of generating high-quality images from text prompts.

### Loading the Model
```python
import dalle_mini

# Initialize Dalle-Mini model
dalle_mini = dalle_mini.DalleModel(model_version=dalle_mini.ModelSize.MEGA) 
```

### Tokenizing the Prompt
The text prompt must be tokenized before it can be used to generate images.
```python
tokenized_prompt = dalle_mini.tokenize_prompt("cat playing with yarn")
```

### Generating Images
Images can be generated from the tokenized prompt.
```python
images = dalle_mini.generate_images(tokenized_prompt, num_predictions=4) 
```

### Decoding Images
The generated images are encoded and must be decoded before they can be displayed.
```python
decoded_images = [Image.fromarray(np.asarray(img * 255, dtype=np.uint8)) for img in images] 
```

### Example Usage
```python
from PIL import Image

# Initialize Dalle-Mini model
dalle_mini = dalle_mini.DalleModel(model_version=dalle_mini.ModelSize.MEGA) 
# Generate images
images = dalle_mini.generate_images("cat playing with yarn", num_predictions=4) 
# Display images
for i, image in enumerate(decoded_images):
     image.save(f"image_{i}.png") 
```

### Additional Information
- The model can be initialized with different model versions (`ModelSize` enum): `MEGA_FULL`, `MEGA`, and `MINI`.
- The number of images to generate can be specified in `num_predictions`.
- The model generates images concurrently on all available GPUs.