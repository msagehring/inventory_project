# Folder structure & README for inventory_project

# Suggested Repo Layout:
# /data/             -> Raw Excel/CSV files, image filenames, JSON exports
# /scripts/          -> Python scripts for automation (rename, sync, convert)
# /shopify/          -> Shopify import/export files (.csv, .xlsx)
# /ms_lists/         -> Microsoft Lists-compatible Excel files
# /docs/             -> Documentation, guides, user notes

# README.md
readme_content = '''

# BSG Inventory Project

Welcome to the official repository for BSG Enterprises' Inventory Management System.
This system supports multi-platform listing (Shopify, eBay, Facebook Marketplace, OfferUp), batch photo handling, Microsoft Lists integration, and auto-generated descriptions.

## 🔖 Folder Structure
```
/data/        - Source files (images, raw intake files, exports)
/scripts/     - Python scripts for renaming, syncing, converting
/shopify/     - Upload-ready Shopify files
/ms_lists/    - Microsoft Lists import templates
/docs/        - How-tos, setup instructions, and team documentation
```

## ✅ Features
- Batch listing generator for multiple platforms
- Microsoft Lists compatibility
- Shopify-ready import files with SEO-optimized descriptions
- Auto-renaming of images using inventory ID format

## 🛠 Setup Instructions
Clone the repo and install requirements:
```bash
git clone https://github.com/msagehring/inventory_project.git
cd inventory_project
pip install -r requirements.txt
```

## 📦 Usage
Add your item photos to `/data/images/`. Then run:
```bash
python scripts/rename_images.py
python scripts/generate_shopify_upload.py
```

## 📁 Generated Files
- `Shopify_Upload_Batch1.xlsx` in `/shopify/`
- `MSLists_Batch1.xlsx` in `/ms_lists/`

---
BSG Enterprises  |  Misfit Musings Production  |  2025
'''

# Python script for renaming images using item IDs
def rename_script():
    return '''
import os
import re

# CONFIGURATION
IMAGE_DIR = './data/images/'
CATEGORY = 'ART'  # Replace or map by batch
START_NUM = 1

# Load filenames and rename
files = sorted(os.listdir(IMAGE_DIR))
id_num = START_NUM
for fname in files:
    if fname.lower().endswith(('.jpg', '.jpeg', '.png')):
        new_name = f"{CATEGORY}-{id_num:04d}_{re.sub(r'[^a-zA-Z0-9]', '-', fname.split('.')[0]).lower()}.jpg"
        os.rename(os.path.join(IMAGE_DIR, fname), os.path.join(IMAGE_DIR, new_name))
        print(f"Renamed: {fname} -> {new_name}")
        id_num += 1
'''

# Output final structure and scripts
print("README.md\n" + readme_content)
print("\nscripts/rename_images.py\n" + rename_script())
