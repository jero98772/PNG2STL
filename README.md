# PNG2STL

**PNG2STL** is a simple web application that allows users to upload a 2D image, convert it into a 3D STL (Stereolithography) model, and then view and download the generated model.  
The application uses **Flask** for the backend and **Three.js** for frontend 3D visualization.

---

## 🚀 Features

- **Image Upload:** Upload common image formats (PNG, JPG, etc.)
- **2D to 3D Conversion:** Converts grayscale intensity to 3D height. Darker areas are extruded; white/transparent areas remain flat.
- **STL Generation:** Creates a standard STL file, compatible with 3D printing software.
- **Interactive 3D Viewer:** View the 3D model in your browser with rotate, pan, and zoom controls.
- **STL Download:** Save the generated STL model locally.

---

## 🧰 Technologies Used

### Backend
- **Python 3** — Core programming language
- **Flask** — Lightweight web framework
- **Pillow** — Image processing
- **NumPy** — Array computations and height map
- **Trimesh** — Mesh creation and STL export

### Frontend
- **HTML5, CSS3, JavaScript** — Web interface and interactivity
- **Three.js** — 3D rendering in browser
- **OrbitControls.js** — Mouse-based camera controls
- **STLLoader.js** — STL file loading in Three.js

---

## ⚙️ Setup and Installation

### 1. Clone the Repository 

```bash
git clone https://github.com/jero98772/PNG2STL
```

### 2. Install Dependencies
Ensure Python 3 is installed, then install required packages:
```bash
pip install Flask Pillow numpy trimesh
```

### 3. Run the Application
Navigate to the project root and start the Flask server:
```bash
python main.py
```
By default, the app runs at: [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

---

## 🖼️ Usage

1. Open your browser and go to: [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
2. Click **Choose File** and upload a PNG or JPG image.
3. Click **Upload and Convert**.
4. Interact with the 3D viewer to rotate, zoom, or pan the model.
5. Click **Download STL** to save the model.
6. Click **Close Viewer** to upload another image.

---

### Screenshots
![](https://raw.githubusercontent.com/jero98772/PNG2STL/refs/heads/main/screenshots/3.png)

![](https://raw.githubusercontent.com/jero98772/PNG2STL/refs/heads/main/screenshots/2.png)

![](https://raw.githubusercontent.com/jero98772/PNG2STL/refs/heads/main/screenshots/1.jpeg)

## 🔍 How the 2D to 3D Conversion Works

The `convert_image_to_stl` function performs the core logic:
- **Grayscale Conversion:** Image is converted to grayscale.
- **Normalization:** Pixel values are scaled to [0.0, 1.0].
- **Height Mapping:**
  ```python
  zz = (1 - arr) * extrusion_scale
  ```
  - White (1.0) → 0.0 mm
  - Black (0.0) → Max height (e.g., 5.0 mm)
  - Grayscale → Intermediate heights

- **Mesh Generation:** Using NumPy to build vertices and `trimesh` to generate faces and export STL.

---

## 🛠️ Customization

- **Extrusion Height:**
  Change `extrusion_scale` in `main.py` to adjust max 3D height.
- **Model Color:**
  Modify the `color` in `THREE.MeshPhongMaterial` in `index.html`.
- **Camera Zoom:**
  Adjust `camera.position.z` and `controls.minDistance` in `index.html` for zoom behavior.

