# WeatherBench Deep Learning Project

This project aims to predict 2-meter temperature (temp2m) using deep learning models applied to meteorological data. We explored various neural network architectures, input variable variations, and hyperparameters to optimize performance.

---

## Project Structure

### 1. **Data**
The data used comes from the **ERA5** dataset and is stored in **Zarr** format. Key characteristics of the data are:
- **Main Variable**: 2-meter temperature (temp2m).
- **Geographical Region**: France.
- **Spatial Resolution**: 1440x720.
- **Temporal Resolution**: 6 hours.
- **Time Periods**:
  - **Training**: 2011-2016.
  - **Validation**: 2018.
  - **Testing**: 2020-2021.

The data is preprocessed to extract temporal sequences:
- **Input**: 6 consecutive timesteps (36 hours of history).
- **Output**: Temperature prediction at the 7th timestep (+6 hours).

---

### 2. **Experiences**
We tested several experiences with different variations to evaluate the performance on the weather forecasting task:

#### **2.1. Nominal Model (Baseline)**
- **Architecture**: Simple 3D CNN with a single convolutional layer.
- **Features**:
  - 1 → 32 filters.
  - Kernel: 3×3×3.
  - Dropout: 0.3.
  - Optimizer: Adam.
  - Loss Function: MSE.
- **Objective**: Serve as a baseline for comparison with more complex models.

#### **2.2. Variation of input variables**
In this experience we variate the input variables; we compare the perfoemance of the model when we have only the temperature at 2m as input and when we add also the wind speed at 10m
#### Constants : 
- **Architecture**: 3D UNet with an encoder-decoder structure.
- **Hyperparameters :**
  - Loss Function : MSE
  - Optimizer :  Adam (lr 1e-4)
- **Epochs :** 50
#### Conclusion
The model performs better when we add the information about the wind speed at 10m in the input.

#### **2.3. Variation of model architecture**
In this part, we compare the performance of the model with different architectures.
#### Constants : 
- **Input**: temperature at 2m + wind speed at 10m.
- **Hyperparameters :**
  - Loss Function : MSE
  - Optimizer :  Adam (lr 1e-4)
- **Epochs :** 50

#### **2.3.1 3D UNet**
- **Architecture**: 3D UNet with an encoder-decoder structure.
- **Features**:
  - Multi-variable: 2m temperature + 10m wind speed.
  - Skip connections to preserve spatial details.
  - Spatial pooling to reduce dimensionality.

#### **2.3.2 ResNet-LSTM**
- **Architecture**: Combination of 3D ResNet for spatio-temporal feature extraction and LSTM for temporal modeling.
- **Features**:
  - Residual blocks to avoid gradient vanishing.
  - LSTM to capture temporal dynamics.

#### **2.3.3 ConvLSTM**
- **Architecture**: ConvLSTM to simultaneously capture spatial and temporal dependencies.
- **Features**:
  - LSTM cells with convolutions to process spatio-temporal data.
  - Multiple stacked layers for better modeling.
#### Conclusion
The model performs better with the 3D UNet architecture.

#### **2.4. Variation of Hyperparameters**
In this part, we compare the performance of the model with different loss functions and optimizers.
#### Constants : 
- **Input**: temperature at 2m + wind speed at 10m.
- **Architecture :** 3D UNet
- **Epochs :** 50

#### Variations :
- Loss functions tested : MSE - MAE
- Optimzers tested : Adam - SGD

#### Conclusion  
The model performs better with the MSE + Adam.

---

### 3. **`outputs` Folder Organization**
The `outputs` folder contains the results of various experiments organized by type of variation:
- `metrics.json`: Metrics results.
- Learning curves
- Prediction examples
- Prediction analysis

To access the data sequences for the following variables:

1. **Temperature at 2 meters (temp2m)**  
2. **Temperature at 2 meters (temp2m) + Wind speed at 10 meters (wind10m)**

Please use the following link:  
[Data Sequences - Google Drive](https://drive.google.com/drive/folders/1w9rt1SuwBB8WlptsjRte6PDAHFIIRQAE?usp=sharing)

## Accessing Best Model Parameters

The parameters of the best-performing model are also available in the same Google Drive folder. You can find the configuration files and metrics used to achieve the best results.
