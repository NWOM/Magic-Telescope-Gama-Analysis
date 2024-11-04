# MAGIC-Gamma-Telescope-Classification
Classification of Gamma and Hadron events by training classifiers and machine learning algorithms on the MAGIC Gamma Telescope dataset.

## Table of Contents
- [Data Set](#data-set)
  * [Attribute Information](#attribute-information)
- [Data Preprocessing](#data-preprocessing)
  * [Data Balancing](#data-balancing)
  * [Data Splitting](#data-splitting)
- [Classification Algorithm](#classification-algorithm)
  * [Neural Network](#neural-network)
- [Classifiers Comparison](#classifiers-comparison)

## Data Set
The [MAGIC gamma telescope dataset](https://archive.ics.uci.edu/ml/datasets/MAGIC+Gamma+Telescope) is generated to simulate registration of high energy gamma particles in a ground-based atmospheric Cherenkov gamma telescope using the imaging technique. The dataset consists of two classes; gammas (signal) and hadrons (background). There are 12332 gamma events and 6688 hadron events.

### Attribute Information
The dataset consists of 10 continuous features and 1 binary class label. The features are listed below:

1. fLength: continuous # major axis of ellipse [mm]
2. fWidth: continuous # minor axis of ellipse [mm]
3. fSize: continuous # 10-log of sum of content of all pixels [in #phot]
4. fConc: continuous # ratio of sum of two highest pixels over fSize [ratio]
5. fConc1: continuous # ratio of highest pixel over fSize [ratio]
6. fAsym: continuous # distance from highest pixel to center, projected onto major axis [mm]
7. fM3Long: continuous # 3rd root of third moment along major axis [mm]
8. fM3Trans: continuous # 3rd root of third moment along minor axis [mm]
9. fAlpha: continuous # angle of major axis with vector to origin [deg]
10. fDist: continuous # distance from origin to center of ellipse [mm]
11. class: g,h # gamma (signal), hadron (background)

## Data Preprocessing
The dataset isn't ready to be used for classification algorithms. It needs to be preprocessed. The preprocessing steps are listed below:

### Data Balancing
The dataset is imbalanced. There are 12332 gamma events and 6688 hadron events. The number of gamma events is much higher than the number of hadron events. This can cause the classifier to be biased towards the gamma events. To solve this problem, the dataset is balanced by downsampling the gamma events to the number of hadron events. The number of gamma events is reduced to 6688.

### Data Splitting
The dataset is split into training and testing sets. The training set is used to train the classifier. The testing set is used to test the classifier. The dataset is split into 80% training set and 20% testing set.

## Classification Algorithm
The classification algorithm used in this project is a Neural Network. The details of the architecture are as follows:

### Neural Network Architecture Details

#### Network Structure
- Input Layer: 10 features (matching the dataset dimensions)
- Hidden Layer 1: 128 neurons with ReLU activation
- Hidden Layer 2: 64 neurons with ReLU activation
- Hidden Layer 3: 32 neurons with ReLU activation
- Output Layer: 1 neuron with Sigmoid activation (for binary classification)

#### Key Components

1. **Activation Functions**
   - Hidden Layers: ReLU (Rectified Linear Unit)
   - Output Layer: Sigmoid (for binary classification output between 0 and 1)

2. **Loss Functions Implemented**
   - Binary Cross-Entropy
   - Hinge Loss
   - Custom Focal Loss (with gamma=2.0, alpha=0.25)

3. **Optimizer**
   - Adam optimizer

#### Training Parameters
- Batch Size: 32
- Epochs: 10
- Validation Split: 20%
- Training/Test Split: 80%/20%

#### Data Preprocessing
- Feature Standardization using StandardScaler
- Class balancing through undersampling
- Binary encoding of target variable (g → 1, h → 0)

#### Model Evaluation
The network is evaluated using:
- Accuracy
- Precision
- Recall
- F1 Score

## Classifiers Comparison
The Neural Network was trained with different loss functions. The performance metrics for each are presented in the table below:

<table align="center">
    <tr>
        <th>Loss Function</th>
        <th>Accuracy</th>
        <th>Precision</th>
        <th>Recall</th>
        <th>F1 Score</th>
    </tr>
    <tr>
        <td>Binary Cross-Entropy</td>
        <td>0.84</td>
        <td>0.85</td>
        <td>0.82</td>
        <td>0.83</td>
    </tr>
    <tr>
        <td>Hinge Loss</td>
        <td>0.84</td>
        <td>0.83</td>
        <td>0.84</td>
        <td>0.84</td>
    </tr>
    <tr>
        <td>Focal Loss</td>
        <td>0.56</td>
        <td>0.53</td>
        <td>1.00</td>
        <td>0.69</td>
    </tr>
</table>
