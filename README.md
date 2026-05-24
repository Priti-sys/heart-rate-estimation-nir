### Heart Rate Estimation from NIR Facial Videos
## Project Overview

This project focuses on estimating Heart Rate (BPM) from Near-Infrared (NIR) facial video frames using signal processing and deep learning techniques.

The complete pipeline includes:

loading NIR image frames
extracting forehead region
generating temporal signal
filtering the signal
estimating BPM
training a CNN-LSTM model for BPM prediction

The project was implemented using PyTorch and the MR-NIRP-D dataset.

Dataset

Dataset Used:
MR-NIRP-D Dataset (NIR modality only)

Dataset Link:

MR-NIRP-D Dataset Download

Dataset Overview:

MR-NIRP-D Dataset Overview

Only the NIR modality was used for this project.

Because the dataset is very large, experimentation was initially performed on a single subject folder (NIR_002) to build and debug the pipeline.

Only a small sample subset is included in this repository.

Technologies Used
Python
OpenCV
NumPy
SciPy
Matplotlib
Scikit-learn
PyTorch

The deep learning pipeline was implemented using the PyTorch framework.

Project Pipeline
NIR Frames
    ↓
Frame Preprocessing
    ↓
Forehead ROI Extraction
    ↓
Signal Generation
    ↓
Signal Smoothing
    ↓
Bandpass Filtering
    ↓
BPM Estimation
    ↓
Sequence Creation
    ↓
CNN + LSTM Model
    ↓
Predicted BPM
Folder Structure
heart_rate_project/
│
├── sample_data/
│      └── NIR_002/
│
├── outputs/
│
├── Heart_Rate_Estimation.ipynb
│
├── README.md
│
└── requirements.txt
Environment Setup

Create virtual environment:

python -m venv venv

Activate environment:

venv\Scripts\activate

Install dependencies:

pip install -r requirements.txt
Main Libraries Used
numpy
pandas
matplotlib
scipy
opencv-python
torch
torchvision
torchaudio
scikit-learn
jupyter
notebook
ipykernel
Running the Project

Start Jupyter Notebook:

jupyter notebook

Open:

Heart_Rate_Estimation.ipynb

Run notebook cells sequentially.

Preprocessing Steps

The following preprocessing steps were applied:

loading .pgm NIR frames
resizing frames
extracting forehead ROI
generating intensity-based temporal signal
Gaussian smoothing
Butterworth bandpass filtering

Initially, MediaPipe was tested for facial landmark extraction, but compatibility issues occurred during implementation. To simplify the workflow, a fixed forehead ROI approach was used.

Ground Truth BPM Preparation

The dataset does not directly provide ready-to-use BPM labels for each sequence. Therefore, BPM values were estimated from the generated signal.

Steps followed:

Forehead region extracted from frames
Average intensity calculated across frames
Temporal signal generated
Signal smoothing applied
Bandpass filtering performed
Peak detection used for BPM estimation

The estimated BPM values were used as labels during training.

Deep Learning Model

A CNN-LSTM model was implemented.

CNN Part

Used for:

extracting spatial features from frames
learning intensity variations

Layers used:

convolution
ReLU activation
max pooling
dropout
LSTM Part

Used for:

learning temporal patterns across sequences
modeling heartbeat-related variations

A Bidirectional LSTM was used during experimentation.

Training Details

Dataset split:

80% Training
10% Validation
10% Testing

Loss Function:

L1 Loss (MAE Loss)

Optimizer:

Adam Optimizer

Learning Rate:

0.0001
Evaluation Metrics

The following metrics were used:

MAE
RMSE
Pearson Correlation

These metrics were used to compare predicted BPM and estimated ground-truth BPM values.

Challenges Faced

Some challenges during implementation:

noisy signal generation
tensor shape mismatch between CNN and LSTM
MediaPipe installation issues
limited BPM variation across labels
large dataset size and training time

Several debugging and optimization steps were required before the full pipeline worked correctly.

Limitations

Current limitations:

experiments performed on limited subjects
fixed ROI instead of adaptive landmark tracking
noisy BPM labels
prediction values became nearly constant because many training samples had similar labels

The main focus of this project was building a complete working pipeline and demonstrating the methodology.

Future Improvements

Possible future improvements:

adaptive ROI extraction
transformer-based temporal models
better BPM label generation
training on larger subject groups
real-time BPM prediction
Final Output

The final output of the system is:

Predicted Heart Rate (BPM)

from a given NIR facial video sequence.

# Project Note

This project was developed as part of a deep learning assignment focused on heart-rate estimation from NIR facial videos using signal-processing and CNN-LSTM based modeling.
