# Custom Image Classification Dataset Loader

## Overview
This project provides a PyTorch-based dataset class for loading and processing image datasets stored in a structured folder format. The dataset class ensures proper distribution of images into **train (70%)**, **validation (20%)**, and **test (10%)** subsets. The dataset is dynamically detected from folder names, making it adaptable for different classification tasks.

## Dataset Structure
The dataset should be organized as follows:
```
data/
    class_1/
        image1.jpg
        image2.jpg
        ...
    class_2/
        image1.jpg
        image2.jpg
        ...
    ...
```

Each folder represents a **class**, and the images inside are instances of that class.

## Installation & Environment Setup
### **1. Clone the Repository**
```bash
git clone https://github.com/your_username/your_repository.git
cd your_repository
```

### **2. Create & Activate a Virtual Environment (Optional but Recommended)**
```bash
python -m venv venv  # Create virtual environment
source venv/bin/activate  # On Mac/Linux
venv\Scripts\activate  # On Windows
```

### **3. Install Required Dependencies**
```bash
pip install -r requirements.txt
```
If `requirements.txt` is not available, manually install the dependencies:
```bash
pip install torch torchvision pillow numpy matplotlib
```

## Usage

### **Using the Dataset in PyTorch**
```python
from torch.utils.data import DataLoader
from custom_dataset import CustomImageDataset  # Import the dataset class

# Define paths and transformations (optional)
data_path = "path/to/data"
transform = None  # You can apply torchvision transforms

# Create dataset instances
train_dataset = CustomImageDataset(data_path, split="train", transform=transform)
valid_dataset = CustomImageDataset(data_path, split="valid", transform=transform)
test_dataset = CustomImageDataset(data_path, split="test", transform=transform)

# DataLoader for batching
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
valid_loader = DataLoader(valid_dataset, batch_size=32, shuffle=False)
test_loader = DataLoader(test_dataset, batch_size=32, shuffle=False)
```

### **Checking Data Integrity**
To verify that no images are duplicated across sets:
```python
assert len(set(train_dataset.images).intersection(valid_dataset.images)) == 0
assert len(set(train_dataset.images).intersection(test_dataset.images)) == 0
assert len(set(valid_dataset.images).intersection(test_dataset.images)) == 0
print("No data leakage detected!")
```

## Acknowledgments
This project was developed as part of a **computer vision and deep learning practice task**. Contributions are welcome! 🚀

## License
This project is licensed under the MIT License - see the `LICENSE` file for details.

