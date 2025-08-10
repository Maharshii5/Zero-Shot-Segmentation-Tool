

# Zero-Shot Infrastructure Auditor 🖼️

This project implements a novel hybrid model for performing zero-shot object detection and segmentation in images. The core idea is to create a powerful tool that can identify and precisely outline any object described in a natural language prompt, even if the model has never seen that specific object during its training.

The primary use case is a simulated "Infrastructure Audit" where you can upload an image (e.g., a satellite photo) and ask the model to find niche, specific items like "solar panel arrays" or "wind turbines" without any re-training. This demonstrates an exceptional level of flexibility and automation for inspection tasks.

## 🌟 Key Features

- **Zero-Shot Detection**: Detects and localizes objects based on a text prompt, not a fixed list of classes.
- **Hybrid Model**: Combines the strengths of Grounding DINO for text-guided bounding box detection and the Segment Anything Model (SAM) for high-precision segmentation masks.
- **Colab-Ready**: The entire project is packaged in a single, runnable script designed for a Google Colab environment with a GPU.
- **Automated Setup**: Automatically installs dependencies and downloads the necessary model weights and configuration files.

## 🛠️ Prerequisites

To run this project, you only need:

- A Google account to access Google Colaboratory.
- An active GPU runtime in your Colab notebook (this is crucial for performance).

## 🚀 How to Use

Follow these simple steps to run the Zero-Shot Auditor in your Colab notebook:

1. Open a new Google Colab notebook.
2. Enable GPU Runtime: Go to `Runtime -> Change runtime type -> select GPU` from the dropdown menu -> click `Save`.
3. Paste the code from the main script into a code cell.
4. Run the cell. The script will automatically:
   - Install all Python library dependencies.
   - Download the Grounding DINO and SAM model weights.
   - Prompt you to upload an image from your local machine.
5. Edit the `target_prompt` variable in the `__main__` block to specify what you want to detect (e.g., "a wind turbine", "a swimming pool", "a crane").
6. The final output will be an image displayed directly in the notebook, with a colored overlay highlighting the segmented objects that were found.

A key part of the process looks like this:

```python
# The actual call to the Grounding DINO model to get bounding boxes.
dino_boxes, _, _ = predict(
    model=dino_model,
    image=image_pil,
    caption=text_prompt,
    box_threshold=0.3,
    text_threshold=0.25
)
