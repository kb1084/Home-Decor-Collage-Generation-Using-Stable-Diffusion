
# 🏡 Home Decor Collage Generation Using Stable Diffusion

This project generates home decor collages using the **Stable Diffusion** model from Hugging Face. The model takes text-based prompts describing home decor setups and generates realistic images, which are then compiled into collages.

---

## 🚀 Features
- 🖼 **Text-to-Image Generation**: Uses Stable Diffusion to create home decor images.
- 🏠 **Customizable Prompts**: Supports various aesthetic themes (e.g., modern, minimalist, cozy).
- 🎨 **Collage Creation**: Combines multiple generated images into a grid-based collage.
- 💾 **Google Drive Integration**: Saves collages for future use.

---

## 📌 Workflow
1. **Model Setup**: Loads Stable Diffusion (`stabilityai/stable-diffusion-2-1`) from Hugging Face.
2. **Prompt Generation**: Dynamically generates prompts describing different home decor styles.
3. **Image Generation**: Uses Stable Diffusion to create images based on prompts.
4. **Collage Creation**: Arranges generated images into a structured collage.
5. **Saving and Displaying**: Saves collages in Google Drive.

---

## 📦 Installation

### 1️⃣ Set Up Google Colab
Since this project runs on **Google Colab**, ensure you have:
- A Google account with **Google Drive access**.

### 2️⃣ Install Required Dependencies
Run the following commands inside a Colab notebook:

```python
!pip install diffusers transformers torch torchvision
```

### 3️⃣ Clone This Repository
```sh
git clone https://github.com/your-username/home-decor-collage.git
cd home-decor-collage
```

---

## 🛠 Usage

### 🌟 Load Stable Diffusion Model
```python
import torch
from diffusers import StableDiffusionPipeline

model_id = "stabilityai/stable-diffusion-2-1"
pipe = StableDiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16)
pipe.to("cuda")
```

### 📝 Define Decor Items & Prompts
```python
home_decor_items = [
    "sofa", "lights", "vases", "curtains", "paintings", "coffee table", 
    "bed", "bookshelves", "rugs", "armchairs", "side tables", "floor lamps"
]

aesthetic_prompts = [
    "a cozy living room with a leather sofa, soft lighting, plants, and a coffee table",
    "a modern bedroom with a large bed, bedside lamps, a rug, and indoor plants"
]
```

### 🎨 Generate Images & Create a Collage
```python
from PIL import Image

# Function to create a collage from a list of images
def create_collage(images, grid_size=(2, 3), image_size=(512, 512)):
    collage_width = grid_size[1] * image_size[0]
    collage_height = grid_size[0] * image_size[1]

    collage = Image.new("RGB", (collage_width, collage_height))

    x_offset = 0
    y_offset = 0

    for i, img in enumerate(images):
        img = img.resize(image_size)
        collage.paste(img, (x_offset, y_offset))

        x_offset += image_size[0]
        if x_offset >= collage_width:
            x_offset = 0
            y_offset += image_size[1]

    return collage
```

### 💾 Save the Collage to Google Drive
```python
from google.colab import drive
drive.mount('/content/drive')

# Generate and save collages
for i in range(10):
    collage = create_collage(num_images=6)
    collage.show()
    collage.save(f"/content/drive/MyDrive/lifesetting_collage_{i+1}.jpg")
```

---

## 📊 Results
- 10 collages generated, each showcasing different home decor setups.
- Images stored in **Google Drive** for easy access.

## 📌 Future Improvements
✅ Increase resolution of generated images  
✅ Experiment with different Stable Diffusion models  
✅ Automate prompt engineering for better home decor styling  



## ✨ Acknowledgments
- Model from **[Hugging Face](https://huggingface.co/stabilityai/stable-diffusion-2-1)**
- **Google Colab** for cloud GPU support  
- Inspiration from interior design datasets and AI image generation

---

## 🔗 Connect
👨‍💻 **Author:** Kaustubh Bhalerao  
📧 Email: [kaustubh.brao@gmail.com](mailto:kaustubh.brao@gmail.com)  
🌐 LinkedIn: [Kaustubh Bhalerao](https://www.linkedin.com/in/kaustubh-bhalerao-566a07258)  

---

Enjoy generating beautiful home decor collages! 🎨🏡✨
