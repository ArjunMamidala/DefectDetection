# DefectDetection
Computer vision system that analyzes images of concrete infrastructure captured by drones and assesses the existence and severity of structural defects like cracks, corrosion, deformation, etc. A complete system wehre civil engineers can upload drone images and the system returns the images with bounding boxes around each detected defect, each labeled with its type, severity score, and a summary report prioritizing the defects that need the most attention. 

## WHY THIS PROBLEM MATTERS
- There are over 600,000 bridges in the US. Roughly one-third of them have structural issues of some sort. 
- Manual inspection requires engineers to physically climb structures, which is expensive, slow, and dangerous.
- Drone-based inspection is growing rapidly, but the bottleneck is that someone still has to manually review thousands of images per inspection.
- Automating defect detection reduces inspection time from days to hours and catches defects humans might miss.
- This is an active area of research and industry investment. Companies like Gecko Robotics, DroneDeploy, and Orbital Insight work in this space.

## THE REAL-WORLD USER

Our users are civil and structural engineers who have just completed a drone flyover of a bridge or building. They have hundreds or thousands of images. They need to know:
1. Which images contain defects?
2. Where exactly are the defects in each image?
3. How severe is each defect?
4. Which defects should they inspect in person first?

## TECH STACK

### Core ML
- **Python 3.10+** — the main language
- **PyTorch** — the framework for all model work.
- **torchvision** — for pre-trained ResNet models, image transforms, data augmentation
- **Ultralytics YOLOv8** — for object detection fine-tuning. Install with `pip install ultralytics`

### Data
- **SDNET2018 dataset** — The primary dataset I'm using in thsi project. Contains 56,000+ images of cracked and non-cracked concrete surfaces (bridge decks, walls, pavements). Download from: https://digitalcommons.usu.edu/all_datasets/48/
- **Roboflow** (free tier, optional) — for dataset management, annotation format conversion, and augmentation. Alternatively, use **LabelImg** for local annotation.
- **OpenCV (cv2)** — image preprocessing, visualization, drawing bounding boxes
- **NumPy** — numerical operations
- **Pandas** — organizing evaluation results

### Backend
- **FastAPI** — REST API for the inference service
- **python-multipart** — for handling image file uploads
- **Uvicorn** — ASGI server for FastAPI

### Frontend
- **React** — for the dashboard.

# Limitations
This system analyzes the defects based on factors that can be determined from a single image such as size, shape, and bounding box size and excludes anything that's beyond the scope of this project, such as load-bearing status and the transformation of the crack over time. 
