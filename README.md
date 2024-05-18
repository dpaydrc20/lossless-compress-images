# lossless-compress-images

### Repository Structure

```
image-compressor/
├── README.md
├── requirements.txt
└── compress_image.py
```

### README.md

```markdown
# Image Compressor

This repository contains a Python script for compressing images to a specified file size.

## Requirements

- Python 3.x
- Pillow

## Installation

1. Clone this repository:
    ```sh
    git clone https://github.com/yourusername/image-compressor.git
    cd image-compressor
    ```

2. Install the required packages:
    ```sh
    pip install -r requirements.txt
    ```

## Usage

To compress an image to a specified size, run the `compress_image.py` script:

```sh
python compress_image.py input_image output_image target_size
```

- `input_image`: Path to the input image file.
- `output_image`: Path to save the compressed image file.
- `target_size`: Target size in KB.

Example:

```sh
python compress_image.py input.jpg output.jpg 25
```
```

### requirements.txt

```
Pillow
```

### compress_image.py

```python
import os
import sys
from PIL import Image

def compress_image(input_path, output_path, target_size_kb):
    image = Image.open(input_path)
    target_size = target_size_kb * 1024  # Convert KB to bytes

    # Perform binary search on the quality to achieve the target file size
    min_quality = 10
    max_quality = 95
    while min_quality <= max_quality:
        quality = (min_quality + max_quality) // 2
        image.save('/tmp/temp_compressed.jpg', 'JPEG', quality=quality)
        file_size = os.path.getsize('/tmp/temp_compressed.jpg')

        if file_size < target_size:
            min_quality = quality + 1
        else:
            max_quality = quality - 1

    # Save the final image
    image.save(output_path, 'JPEG', quality=max_quality)
    print(f"Image saved to {output_path} with quality {max_quality}")

if __name__ == "__main__":
    if len(sys.argv) != 4:
        print("Usage: python compress_image.py input_image output_image target_size")
        sys.exit(1)

    input_image = sys.argv[1]
    output_image = sys.argv[2]
    target_size_kb = int(sys.argv[3])

    compress_image(input_image, output_image, target_size_kb)
```

### Instructions

1. Create a new repository on GitHub.
2. Clone the repository to your local machine.
3. Add the above files to the repository directory.
4. Commit the changes and push to GitHub.

```sh
git add .
git commit -m "Initial commit"
git push origin main
```

This will create a GitHub repository with a script for compressing images to a specified file size.
