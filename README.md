# Autonomous Nano Car

Built an autonomous toy car on **Jetson Nano** by leveraging **CUDA GPU acceleration** and **TensorRT optimization** to overcome limited computing resources and accelerate **real-time inference**.

## Highlights

- **End-to-end self-driving** – a camera feeds a neural network that directly outputs steering and throttle.
- **TensorRT FP16 optimization** – the PyTorch model is auto-converted to a TensorRT engine for fast on-device inference.
- **CUDA acceleration** – the full inference loop runs on the Nano's GPU, making real-time control possible on a 4GB edge device.
- **Complete ML pipeline** – data collection → training → deployment, all on embedded hardware.

Based on NVIDIA's [JetRacer](https://github.com/NVIDIA-AI-IOT/jetracer).

![NanoCar](https://github.com/claudwq/NanoCarProject/assets/75829668/03e8ad2a-05a8-41bf-ba70-80b8298d3be0)

---

## How It Works

```
Camera  ──►  Neural Network  ──►  Steering + Throttle  ──►  Car moves
```

1. **Collect** – drive the car yourself and record camera images.
2. **Train** – teach a model to copy your driving.
3. **Drive** – the model drives the car on its own.

---

## Hardware

| Part | Model |
|------|-------|
| Brain | Jetson Nano 4GB Developer Kit (B01) |
| Camera | IMX219, 160° wide-angle |
| Chassis | JetRacer kit |

---

## Quick Start

### 1. Collect data
Open `autopilot_data_collection.ipynb` in Jupyter and record your driving.

### 2. Train the model
Open `autopilot_training.ipynb` and run all cells. This saves a `.pth` model file.

### 3. Let it drive
Set your model path at the top of `autopilot_testing.py`:
```python
MODELS_DIR = "models/"
NAME = "my_model"
```
Then run:
```bash
python3 autopilot_testing.py
```
The first run converts the model to **TensorRT** for faster speed (takes a few minutes, only once).

Press **Ctrl + C** to stop the car.

---

## Files

| File | What it does |
|------|--------------|
| `autopilot_data_collection.ipynb` | Record driving data |
| `autopilot_training.ipynb` | Train the model |
| `autopilot_testing.py` | Run self-driving on the car |
| `autopilot_model.py` | Model definition |
| `autopilot_dataset.py` | Loads training data |
| `autopilot_utils.py` | Image helpers (crop, preprocess) |

---

## Tuning

Change these in `autopilot_testing.py`:

| Setting | Meaning |
|---------|---------|
| `THROTTLE_GAIN` | Max speed (0–1) |
| `STEERING_OFFSET` | Fix if the car drifts left/right |
| `SHOW_LOGS` | `True` to print FPS, steering, throttle |

---

## License
GPL-3.0
