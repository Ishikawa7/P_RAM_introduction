## Application Overview

The **P_RAM** is a sophisticated web-based malware analysis dashboard built using Python's Dash framework. It's designed for cybersecurity professionals to analyze, classify, and detect anomalies in malware samples using advanced machine learning techniques.

## Main Architecture Components

### Core Technologies
- **Frontend**: Dash with Bootstrap components (Sandstone theme)
- **Backend**: Python with pandas, scikit-learn, TensorFlow
- **Machine Learning**: TOCAT model, Self-Organizing Maps (SOM), Anomaly Detection
- **Data Processing**: Pandas for data manipulation and analysis

### Key Machine Learning Models
1. **TOCAT** - Custom ensemble machine learning model for classification
2. **SOM (Self-Organizing Maps)** - For data visualization and clustering
3. **Anomaly Detection Model** - For identifying outliers and unusual patterns

## Application Views and Functionalities

**Main Dashboard and Data Upload Hub**

**Key Features:**
- **File Upload Interface**: Upload new malware CSV files for analysis
- **P_RAM Analysis Launcher**: Execute the complete analysis pipeline
- **Data Management**: Delete last acquisition functionality
- **Statistical Overview**: Pie charts showing:
  - Distribution of malware classes in the entire dataset
  - Distribution of newly uploaded malware samples
- **Real-time Feedback**: Status messages for upload validation and analysis progress

**Workflow:**
1. Upload CSV file with 65 required features + metadata (FireEye labels, ThreatConnect labels, Hash IDs)
2. File validation (format, columns, null values, duplicate IDs)
3. Launch comprehensive analysis pipeline
4. View updated statistics

**Malware Classification Analysis**

**Key Features:**
- **Global Accuracy Metrics**: Overall classification performance statistics
- **Accuracy Trends**: Time-series visualization of classification accuracy
- **Classification Statistics**: 
  - Correctly classified samples
  - Misclassified samples
  - Accuracy breakdown by model (FireEye vs ThreatConnect)
- **Individual Sample Search**: Search by malware ID to view:
  - Classification scores bar chart
  - Detailed sample information table
- **Expandable Accuracy Timeline**: Interactive chart showing accuracy evolution over time

**Self-Organizing Map Visualization**

**Key Features:**
- **Interactive SOM Map**: 2D scatter plot visualization where:
  - Each point represents a malware sample
  - Colors indicate malware families (FireEye labels)
  - Proximity indicates similarity
  - Click functionality for detailed analysis
- **Topographic Error Display**: SOM quality metric
- **Sample Analysis Tools**:
  - ID-based search functionality
  - Detailed classification scores for selected samples
  - Principal component visualization
- **Class Distribution Visualization**: "Pallogramma" showing class distribution across the SOM

**SOM Interpretation:**
- Similar malware samples cluster together
- Distance from Best Matching Unit (BMU) indicates classification confidence
- Visual pattern recognition for malware families

**Anomaly Detection and Outlier Analysis**

**Key Features:**
- **Recent Malware Display**: Latest uploaded samples
- **Anomalous Sample Identification**: Samples with high anomaly scores
- **Interactive Visualizations**:
  - Scatter plot of anomalies (samples with score > 55)
  - Complete anomaly score distribution
  - Time-series analysis with moving averages
- **Search Functionality**: ID-based anomaly investigation
- **Anomaly Metrics**: 
  - Anomaly scores
  - Outlier classification (binary)
  - Temporal trends

## Core Data Processing Pipeline (P_RAM_ops.py)

### The `run_PRAM_ops()` Function Workflow:

1. **Data Preprocessing**: Index setting and feature selection
2. **TOCAT Classification**: 
   - Model 1: For FireEye-labeled samples
   - Model 2: For generic/ThreatConnect samples
3. **Database Updates**: Prediction database maintenance
4. **SOM Analysis**: 
   - Feature scaling and normalization
   - Best Matching Unit (BMU) identification
   - Distance calculations
5. **Anomaly Detection**: Outlier identification and scoring
6. **Model Retraining**: Continuous learning with new data
7. **Data Persistence**: Save updated models and databases

## Data Management

### Input Data Structure:
- **65 Feature Columns**: Malware characteristics for ML analysis
- **Metadata Columns**:
  - FireEye_label: Primary classification label
  - ThreatConnect_label: Secondary classification label
  - ID: Unique identifier (SHA hash)
  - Acquisition date and processing flags

### Output Data:
- **Classification Results**: Semeion_label predictions
- **SOM Coordinates**: X_som, Y_som positions
- **Anomaly Metrics**: Scores and outlier flags
- **Confidence Measures**: Distance from BMU, classification probabilities

## Technical Specifications

### Performance Features:
- **Background Processing**: Long-running analysis tasks
- **Caching**: Efficient data loading with class-based data management
- **Scalability**: Modular architecture for easy expansion
- **Error Handling**: Comprehensive exception management

### Security and Reliability:
- **Input Validation**: Robust CSV file checking
- **Data Integrity**: Duplicate detection and consistency checks
- **Model Persistence**: Automatic model saving and loading
- **Backup Systems**: Data reserve directories for recovery

This application represents a comprehensive malware analysis platform that combines multiple machine learning techniques to provide cybersecurity professionals with powerful tools for malware classification, anomaly detection, and pattern recognition through intuitive web-based visualizations.
