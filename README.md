# EPG-DTPNet: Extreme-value Prior-Guided Dual-Branch Deep Temporal Prediction Network
Official TensorFlow implementation of the extreme-value prior-guided dual-branch deep temporal prediction network for displacement time-history prediction of CFST (Concrete-Filled Steel Tubular) members under transverse impact loading.

---

## 📖 Introduction
Accurate prediction of structural dynamic response under impact loading is critical for the impact-resistant design of CFST structures. This work proposes EPG-DTPNet, a dual-branch deep temporal prediction network guided by extreme-value prior. The model decouples the waveform shape and amplitude of displacement time-history through a two-branch architecture, and introduces a physically constrained composite loss function to ensure the physical rationality of prediction results.

The model takes static physical parameters of CFST members and pre-predicted peak displacement as inputs, and outputs the full displacement time-history curve under impact loading. It combines the advantages of signal decomposition, temporal deep learning and physical prior guidance, and achieves high prediction accuracy on transverse impact response prediction tasks.

## 🛠️ Environment Requirements
### Core Dependencies (Mandatory for Algorithm Running)
| Library | Required Version | Description |
| :--- | :--- | :--- |
| Python | 3.8 ~ 3.10 | Runtime environment (fully compatible with TensorFlow 2.8.x) |
| TensorFlow | 2.8.0 | Deep learning framework |
| tensorflow-gpu | 2.8.0 | GPU acceleration support (optional but highly recommended) |
| CatBoost | 1.2.10 | Pre-trained extreme-value prior prediction model |
| NumPy | 1.26.4 | Fundamental numerical computation |
| Pandas | 2.3.3 | Tabular data processing |
| scikit-learn | 1.5.2 | Data normalization and metric calculation |
| SciPy | 1.13.1 | Scientific computation support |
| Matplotlib | 3.5.1 | Result visualization |
| vmdpy | 0.2 | Variational mode decomposition implementation |
| Joblib | 1.4.2 | Model and scaler serialization |
| OpenPyXL | 3.1.5 | Excel result export |
| Optuna | 4.1.0 | Hyperparameter optimization (optional) |

### GPU Acceleration Configuration
To enable GPU training, please install **CUDA 11.2** and **cuDNN 8.1** in advance, which are the official matching versions for TensorFlow 2.8.0.

---

## 🚀 Quick Start
### 1. Clone the Repository
```bash
git clone https://github.com/zhongxueqi/EPG-DTPNet.git
cd EPG-DTPNet
```

### 2. Install Core Dependencies
```bash
pip install tensorflow==2.8.0 catboost==1.2.10 numpy==1.26.4 pandas==2.3.3 scikit-learn==1.5.2 scipy==1.13.1 matplotlib==3.5.1 vmdpy==0.2 joblib==1.4.2 openpyxl==3.1.5
```

### 3. Prepare Dataset and Pre-trained Model
1.  Organize your dataset into CSV format: the first 10 columns are sample metadata and physical parameters, and the subsequent columns are displacement time-history data at each time step.
2.  Pre-train a CatBoost model for peak displacement prediction, and save the model file.
3.  Split the dataset into training, validation and test sets in advance, named `NN_Pretrain_Train.csv`, `NN_Pretrain_Val.csv` and `NN_Pretrain_Test.csv` respectively.

### 4. Configure Parameters
Modify the `experiment_config` dictionary in `EPG-DTPNet.py`:
- `dataset_dir`: Absolute path to your dataset folder
- `catboost_max_path`: Absolute path to the pre-trained CatBoost peak prediction model
- Adjust hyperparameters such as `K_modes`, network units, loss weights and training epochs as needed.

### 5. Run the Full Pipeline
```bash
python EPG-DTPNet.py
```

---

## 📁 Project Structure
```
EPG-DTPNet/
├── 01-VMD_DualBranch_Vec2Seq16.py    # Main script: full training & evaluation pipeline
├── Results.zip                        # Calculation results
└── README.md                         # Project documentation
```

### Core Modules in Main Script
1.  **Global deterministic seed setting**: Ensure fully reproducible experiments
2.  **Enhanced gradient MSE loss**: Physically constrained composite loss function with multi-dimensional regularization
3.  **VMD data preprocessing**: Signal decomposition, padding and component-wise normalization
4.  **Dual-branch network construction**: EPG-DTPNet model definition with configurable attention type
5.  **Training pipeline**: Model training with early stopping and cosine annealing learning rate schedule
6.  **Post-processing & evaluation**: IMF reconstruction, metric calculation and batch result visualization

---


## 📊 Output Results
After running the script, all results will be saved to the automatically generated `output_Original_Plots_YYYYMMDD_HHMMSS` folder, including:
- Training and validation loss curve
- VMD decomposition example plot
- Comparison plots of predicted and true displacement curves for validation and test sets
- Training report with detailed metrics (MSE, RMSE, MAE, R²) at both sample-wise and global levels
- Excel file containing raw prediction data and training history

---

## 📝 Citation
If you use this code or the proposed method in your research, please cite our paper as follows:
```
[Paper citation information will be updated after publication]
```
