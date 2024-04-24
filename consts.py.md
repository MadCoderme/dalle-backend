## 🔗 Table of Contents ##

- [Introduction](#introduction)
- [DALL-E Mini Model Options](#dalle-e-mini-model-options)
- [VQGAN Model Options](#vqgan-model-options)
- [Generation Parameters](#generation-parameters)
- [Example Usage](#example-usage)

## 📖 Introduction ##

This document provides a detailed overview of the various model options and generation parameters used in our DALL-E Mini-based image generation system. Understanding these options is crucial for achieving optimal results and tailoring image generation to specific requirements.

## 🎨 DALL-E Mini Model Options ##

| Model Name | Description |
|---|---|
| `DALLE_MODEL_MINI` | The original DALL-E Mini model, offering a balance between speed and quality. |
| `DALLE_MODEL_MEGA` | An advanced version of DALL-E Mini, providing higher-quality images at the cost of increased computation time. |
| `DALLE_MODEL_MEGA_FULL` | The most powerful DALL-E Mega model, capable of generating exceptionally detailed and realistic images but requiring significant storage and GPU memory. |

## 📸 VQGAN Model Options ##

| Model Name | Description |
|---|---|
| `VQGAN_REPO` | The repository name of the VQGAN model used for image generation. |
| `VQGAN_COMMIT_ID` | The specific commit ID within the VQGAN repository to use, ensuring reproducibility. |

## ⚙️ Generation Parameters ##

| Parameter | Description |
|---|---|
| `GEN_TOP_K` | Controls the number of top tokens to consider during generation. Higher values promote diversity, while lower values favor coherence. |
| `GEN_TOP_P` | Specifies the probability distribution of tokens to consider during generation. Higher values favor common tokens, while lower values increase randomness. |
| `TEMPERATURE` | Adjusts the randomness of the generated images. Higher values lead to more unexpected and creative results, while lower values produce more predictable images. |
| `COND_SCALE` | Influences the strength of the conditioning text on the generated images. Higher values emphasize the text, while lower values allow for more freedom in interpretation. |

## 🚀 Example Usage ##

```python
from dalle_mini import DalleMini

# Initialize the DalleMini model with the desired options
dalle_mini = DalleMini(model=DALLE_MODEL_MEGA)

# Generate an image from a text prompt
image = dalle_mini.generate(prompt="A cat wearing a cowboy hat")

# Save the generated image
image.save("cat_in_hat.png")
```

Please note that the availability of specific model options and generation parameters may vary depending on the version of the DALL-E Mini library and underlying infrastructure. Consult the official documentation for the latest information.