# Visinory-forge-AI---text-to-image
Visionary Forge AI — elegant web UI + backend for high-quality text→image generation.

# AI-Powered Text-to-Image Generator

A web application that generates images from text descriptions using Stable Diffusion and Flask.

## Features

- 🎨 Generate images from text prompts
- 🔧 Adjustable inference steps and guidance scale
- 🚫 Negative prompt support
- 💾 Download generated images
- 🎯 User-friendly web interface
- ⚡ GPU acceleration support

## Project Structure

```
text-to-image-generator/
├── app.py                  # Flask backend
├── requirements.txt        # Python dependencies
├── templates/
│   └── index.html         # Frontend HTML/CSS/JS
└── README.md              # This file
```

## Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- (Optional) CUDA-capable GPU for faster generation

## Installation

### 1. Clone or Create Project Directory

```bash
mkdir text-to-image-generator
cd text-to-image-generator
```

### 2. Create Virtual Environment (Recommended)

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

**Note:** The first time you run the application, it will download the Stable Diffusion model (~4GB). This is a one-time download.

### 4. Create Directory Structure

```bash
mkdir templates
mkdir static
```

### 5. Add the Files

- Save `app.py` in the root directory
- Save `index.html` in the `templates/` directory
- Save `requirements.txt` in the root directory

## Usage

### 1. Start the Flask Server

```bash
python app.py
```

The server will start on `http://localhost:5000`

### 2. Open in Browser

Navigate to `http://localhost:5000` in your web browser.

### 3. Generate Images

1. Enter a descriptive prompt (e.g., "A beautiful sunset over mountains")
2. (Optional) Add negative prompts to avoid unwanted features
3. Adjust inference steps (20-100, higher = better quality but slower)
4. Adjust guidance scale (1-20, higher = closer to prompt)
5. Click "Generate Image"
6. Wait 30-60 seconds for generation
7. Download your image!

## Configuration

### Model Selection

By default, the app uses `runwayml/stable-diffusion-v1-5`. You can change this in `app.py`:

```python
model_id = "runwayml/stable-diffusion-v1-5"  # Change to your preferred model
```

### Image Size

Default is 512x512. Modify in `app.py`:

```python
image = model(
    prompt=prompt,
    height=512,  # Change height
    width=512,   # Change width
    ...
)
```

### Port Configuration

Change the port in `app.py`:

```python
app.run(debug=True, host='0.0.0.0', port=5000)  # Change port here
```

## Performance Tips

### GPU Acceleration

- If you have a CUDA-capable GPU, the app will automatically use it
- GPU generation is 10-20x faster than CPU
- Check if GPU is detected: visit `http://localhost:5000/health`

### CPU-Only Mode

- If no GPU is available, the app runs on CPU
- First generation takes 2-5 minutes
- Subsequent generations: 1-3 minutes
- Consider using fewer inference steps (20-30) for faster results

### Memory Requirements

- GPU: Minimum 6GB VRAM (8GB+ recommended)
- CPU: Minimum 8GB RAM (16GB+ recommended)

## Troubleshooting

### Model Download Issues

If the model fails to download:
```bash
# Clear cache and retry
rm -rf ~/.cache/huggingface/
python app.py
```

### Out of Memory Error

- Reduce inference steps
- Use CPU instead of GPU (modify `app.py`)
- Close other applications
- Reduce image size

### Port Already in Use

```bash
# Change port in app.py or kill the process
# On Linux/Mac
lsof -ti:5000 | xargs kill -9

# On Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

### Import Errors

```bash
# Reinstall dependencies
pip uninstall -y -r requirements.txt
pip install -r requirements.txt
```

## API Endpoints

### POST /generate

Generate an image from a prompt.

**Request Body:**
```json
{
  "prompt": "A beautiful landscape",
  "negative_prompt": "blurry, low quality",
  "steps": 50,
  "guidance_scale": 7.5
}
```

**Response:**
```json
{
  "success": true,
  "image": "data:image/png;base64,...",
  "prompt": "A beautiful landscape"
}
```

### GET /health

Check server health and GPU availability.

**Response:**
```json
{
  "status": "healthy",
  "cuda_available": true,
  "model_loaded": true
}
```

## Example Prompts

**Good prompts are detailed and descriptive:**

- "A serene mountain landscape at sunset with purple sky, reflecting in a crystal clear lake, photorealistic, 4k quality"
- "Portrait of a wise old wizard with a long white beard, wearing blue robes, holding a magical staff, fantasy art style"
- "Futuristic cyberpunk city at night, neon lights, flying cars, rain, cinematic lighting"

**Use negative prompts to improve quality:**

- "blurry, low quality, distorted, ugly, bad anatomy, watermark, text"

## Technologies Used

- **Backend:** Flask, Python
- **AI Model:** Stable Diffusion (via Hugging Face Diffusers)
- **Deep Learning:** PyTorch, Transformers
- **Frontend:** HTML5, CSS3, JavaScript

## License

This project is for educational purposes. The Stable Diffusion model has its own license terms.

## Credits

- Stable Diffusion by Stability AI
- Hugging Face Diffusers library
- Flask web framework

## Support

For issues and questions:
- Check the Troubleshooting section
- Visit Hugging Face documentation: https://huggingface.co/docs/diffusers
- Flask documentation: https://flask.palletsprojects.com/

---

**Enjoy creating AI-generated art! 🎨✨**
