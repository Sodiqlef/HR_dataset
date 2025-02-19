# HR Data Cleaning and Visualization Project

This project focuses on cleaning and visualizing an HR dataset. The dataset contains employee information such as name, age, salary, gender, department, position, joining date, and performance score. Additionally, the `joining date` column was used to extract the `year` and `month` for further analysis. The cleaned data is then visualized to uncover insights about the workforce.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Requirements](#requirements)
4. [Steps](#steps)
   - [Data Cleaning](#data-cleaning)
   - [Feature Engineering](#feature-engineering)
   - [Data Visualization](#data-visualization)
5. [Results](#results)
6. [How to Run](#how-to-run)
7. [License](#license)

---

## Project Overview
This project involves cleaning an HR dataset to handle missing values, inconsistencies, and outliers. Feature engineering is performed to extract the `year` and `month` from the `joining date`. Finally, the data is visualized to analyze trends in employee demographics, performance, and department-wise distribution.

---

## Dataset
The dataset contains the following columns:
- **Name**: Employee name
- **Age**: Employee age
- **Salary**: Employee salary
- **Gender**: Employee gender (e.g., Male, Female)
- **Department**: Department the employee belongs to (e.g., HR, IT, Sales)
- **Position**: Employee job title
- **Joining Date**: Date the employee joined the company
- **Performance Score (Grade)**: Employee performance score (e.g., A, B, C)

Additionally, two new columns were created:
- **Joining Year**: Extracted year from the `Joining Date`
- **Joining Month**: Extracted month from the `Joining Date`

---

## Requirements
To run this project, you need the following Python libraries:
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`

Install the required libraries using:
```bash
pip install pandas numpy matplotlib seaborn
```

---

## Steps

### Data Cleaning
1. **Load the Dataset**:
   - Use `pandas` to load the dataset into a DataFrame.
   ```python
   import pandas as pd
   df = pd.read_csv('data/hr_dataset.csv')
   ```

2. **Handle Missing Values**:
   - Identify missing values using `df.isnull().sum()`.
   - Fill or drop missing values based on the context.
   ```python
   df.fillna(method='ffill', inplace=True)  # Forward fill
   # OR
   df.dropna(inplace=True)  # Drop rows with missing values
   ```

3. **Remove Duplicates**:
   - Remove duplicate rows to ensure data integrity.
   ```python
   df.drop_duplicates(inplace=True)
   ```

4. **Handle Outliers**:
   - Detect and handle outliers in numerical columns like `Age` and `Salary`.
   ```python
   from scipy import stats
   df = df[(np.abs(stats.zscore(df['Salary'])) < 3)]
   ```

5. **Data Transformation**:
   - Convert data types if necessary (e.g., `Joining Date` to datetime).
   ```python
   df['Joining Date'] = pd.to_datetime(df['Joining Date'])
   ```

---

### Feature Engineering
1. **Extract Year and Month**:
   - Create new columns for `Joining Year` and `Joining Month`.
   ```python
   df['Joining Year'] = df['Joining Date'].dt.year
   df['Joining Month'] = df['Joining Date'].dt.month
   ```

2. **Map Performance Scores**:
   - Create performance grades to convert performance score  to numerical values for analysis.
   ```python
   performance_map = {'A': 4, 'B': 3, 'C': 2, 'D': 1}
   df['Performance Grade'] = df['Performance Score'].map(performance_map)
   ```

---

### Data Visualization
1. **Employee Distribution by Department**:
   - Visualize the number of employees in each department.

2. **Salary Distribution**:
   - Analyze the distribution of salaries using a histogram or boxplot.
   

3. **Performance by Gender**:
   - Compare performance scores across genders.

4. **Joining Trends Over Time**:
   - Visualize the number of employees joining each year or month.

5. **Age vs. Salary**:
   - Explore the relationship between age and salary.
  

---

## Results
After cleaning and visualizing the data, the following insights were uncovered:
- **Insight 1**: The Finance department has the highest number of employees.
- **Insight 2**: Performance scores do not necessarily correlate with salary levels.
- **Insight 3**: Most employees joined in the year 2020.
- **Insight 4**: The male gender is the most employed
Visualizations are saved in the `plots/` folder.

---

## How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/hr-data-cleaning-visualization.git
   ```
2. Navigate to the project directory:
   ```bash
   cd hr-data-cleaning-visualization
   ```
3. Install the required libraries:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
4. Run the Jupyter Notebook or Python script:
   ```bash
   jupyter notebook hr_data_analysis.ipynb
   # OR
   python hr_data_analysis.py
   ```

---


Feel free to contribute or suggest improvements!
