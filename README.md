# 353 Project: Go-Pro Data Analysis

## Description
This project aims to analyze gyroscope data collected from Go-Pro cameras to classify various tricks performed in sports activities. The key features include data preprocessing, model training using machine learning algorithms, and visualization of gyroscope data.

## Installation
1. Ensure the following Python libraries are installed:
   - pandas
   - numpy
   - sklearn
   - scipy
   - matplotlib
   - os
   - zipfile
2. Download the following files in a folder accessible to the Jupyter Notebook environment:
   - Load.ipynb
   - Analysis.ipynb
   - GoPro_Data.zip
3. Set the current working directory to the folder containing the listed files if not done already.

## Usage
1. Run Load.ipynb:
   - This notebook automatically decompresses "GoPro_Data.zip" and executes without any required inputs.
   - Generates "features_data.csv" and gyroscope data graphs saved in the script and dataset folder.
2. Run Analysis.ipynb:
   - Utilizes "features_data.csv" (generated by Load.ipynb) as its primary dataset.
   - Trains multiple machine learning models and provides training/validation scores for each model.

## Technical Documentation
- **Libraries**:
   - Data Preprocessing: Utilized Python Pandas and NumPy for data cleaning and organization.
   - Visualization: Employed Matplotlib for gyroscope plots.
   - Machine Learning: Utilized Scikit-learn library for model training and feature importance analysis.
   - Imported libraries: os (for handling file paths), zipfile (for handling zip file folders).
   
- **Load.ipynb**:
   - **Functions**:
       - **calculate_means(df)**:
           - Divides the given DataFrame into 30 equal sections.
           - Computes mean values for specific columns ('1', '2', 'Gyroscope [rad/s]') in each section.
           - Returns a list of means for each column.
       - **transform(trick_name, trick_folder_path)**:
           - Processes CSV files in a specified folder path related to a specific trick.
           - Utilizes the calculate_means function to compute means for gyroscope readings.
           - Forms a list of mean values along with the trick name.
           - Returns a collection of mean data for a particular trick.
       - **process_master_folder(master_folder_path)**:
           - Processes all subfolders (representing different tricks) within a master folder.
           - Calls the transform function for each trick subfolder to gather mean data.
           - Returns a collection of mean data for all tricks in the master folder.
       - **plot_data(features_df, plot_individual=True)**:
           - Generates a plot displaying gyroscope data for each trick individually or their mean values.
           - Uses Matplotlib to plot gyroscope feature values against feature index.
           - Customizes colors and plot styles based on trick names and whether to show individual or mean plots.
       - **unzip_file(zip_file_name, extract_dir)**:
           - Extracts files from a specified ZIP file into a directory.
           - Checks if the extraction directory exists and creates it if not.
           - Unzips the file into the specified directory.

   - **Main Function (main())**:
       - Unzips GoPro_Data.zip into a folder named GoPro_Data.
       - Processes the GoPro_Data folder by calling process_master_folder.
       - Converts the gathered mean data into a Pandas DataFrame (features_df).
       - Saves this DataFrame as a CSV file named features_data.csv.
       - Calls plot_data function twice to generate and save gyroscope data plots (individual and mean plots) based on the created DataFrame.

   - **Overall Functionality**:
       - Extracts gyroscope data from CSV files in different trick folders within a master folder.
       - Calculates means for specific columns in the gyroscope data.
       - Generates visualizations to display gyroscope data for individual tricks and their mean values.
       - Saves the processed gyroscope data as a CSV file for further analysis.
 
- **Analysis.ipynb**:
   - **Class: TrickClassifier**
       - **__init__ Method**:
           - Loads data from a specified CSV file (data_path).
           - Initializes training and validation data variables (X_train, X_valid, y_train, y_valid) as None.
           - Sets a random seed (random_state) for reproducibility in data splitting.
       - **split_data Method**:
           - Splits loaded data into training and validation sets for supervised learning.
           - Separates data into different trick categories and randomly shuffles them.
           - Divides each category into subsets based on the train_size parameter.
           - Prepares X_train, X_valid, y_train, and y_valid for model training and evaluation.
       - **train_model Method**:
           - Trains a machine learning model (model) using provided training data (X_train, y_train).
           - Evaluates the trained model's performance on both training and validation datasets (X_valid, y_valid).
           - For RandomForestClassifier, extracts feature importances and plots a bar graph showcasing these importances.

   - **Main Execution**:
       - Reads the CSV file (features_data.csv) containing gyroscope readings data.
       - Instantiates TrickClassifier, splits data, initializes machine learning models, trains models, and prints scores.
       - Includes a commented-out section for hyperparameter tuning (GridSearchCV) intended for RandomForestClassifier but currently not executed in this script.
