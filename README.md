# 📏 Object Size Measurement using Computer Vision

An interactive, AI-powered Flask web application that automatically calculates the dimensions (width and height in centimeters) of objects in an uploaded image. Powered by **OpenCV** and **NumPy**.

![Interface Preview](Interface%20layout%20image.png)

---

## 🌟 Features

* 🪙 **Automatic Reference Calibration**: Automatically uses the first detected object (like a coin of standard 2.5 cm diameter) as a calibration reference to calculate the `pixels-to-cm` ratio.
* 📏 **Precise Size Annotation**: Detects and contours surrounding objects, calculating and displaying their width and height dynamically on the output image.
* 🎨 **Premium UI/UX Design**: Includes a modern, glassmorphic layout, drag-and-drop image upload, real-time feedback, and dynamic progress loaders.
* ⚡ **Fast & Robust Pipeline**: Uses Canny edge detection, Gaussian blurring, and morphological operations (dilation and erosion) for reliable contour mapping.

---

## 🛠️ Tech Stack

* **Backend**: Python, Flask
* **Image Processing**: OpenCV (Open Source Computer Vision Library), NumPy
* **Frontend**: HTML5, Vanilla CSS3 (Modern Flexbox/Grid, gradients, and micro-animations), JavaScript (ES6 Fetch API)

---

## ⚙️ How It Works (The CV Pipeline)

1. **Preprocessing**: The uploaded image is converted to grayscale and smoothed using a Gaussian blur ($7 \times 7$ kernel) to filter out background noise.
2. **Edge Detection**: A Canny edge detector is applied, followed by dilation and erosion to bridge gaps in the detected edges.
3. **Contour Extraction**: External contours are extracted and sorted based on their location and area size.
4. **Reference Calibration**: The first contour found is designated as the reference object (with a predefined physical size of $2.5\text{ cm}$). The code calculates:
   $$\text{pixels\_per\_cm} = \frac{\text{Width in pixels}}{\text{Reference width in cm}}$$
5. **Measurement & Output**: For all subsequent contours, dimensions are calculated using the calibrated ratio and mapped back onto the image with bounding boxes.

---

## 🚀 Getting Started

### Prerequisites

* Python 3.8 or higher installed on your system.

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Nandeesh-06/Object-Size-Measurement-using-CV.git
   cd Object-Size-Measurement-using-CV
   ```

2. **Set up a Virtual Environment**:
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install flask opencv-python numpy
   ```

4. **Run the Application**:
   ```bash
   python app.py
   ```

5. Open your browser and navigate to `http://127.0.0.1:5000` to start measuring!

---

## 📂 Project Structure

```text
Object-Size-Measurement-using-CV/
│
├── app.py                # Main Flask application and OpenCV logic
├── templates/
│   └── index.html        # Front-end UI (upload interface & results)
├── Inputs images/        # Directory containing sample images
├── Output images/       # Directory containing sample outputs
├── uploads/              # Directory for temp uploaded files (ignored by Git)
├── outputs/              # Directory for temp processed images (ignored by Git)
├── .gitignore            # Git exclusion rules
└── README.md             # Project documentation
```

---

## 💡 Calibration Customization

If your reference object is not a 2.5 cm coin, you can change the reference width in `app.py`:

```python
REFERENCE_WIDTH_CM = 2.5  # Adjust this value to match your reference object's width (in cm)
```
*Note: Make sure your reference object is the leftmost/first detected object in the image for the calibration logic to align correctly.*
