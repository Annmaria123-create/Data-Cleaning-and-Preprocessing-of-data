# Data-Cleaning-and-Preprocessing-of-data
# Medical Appointment No-Show Dataset

This dataset contains information on medical appointments and whether patients showed up for their appointment in Brazil.

## 📊 Dataset Overview

- **Rows:** ~110K appointments  
- **Columns:** 14 features
- **Source:** Public healthcare system of Vitória, Brazil.

| Column Name        | Description                                                |
|--------------------|------------------------------------------------------------|
| patientid          | Unique identifier for the patient.                         |
| appointmentid      | Unique identifier for the appointment.                     |
| gender             | Gender of the patient (`Male`, `Female`).                  |
| scheduledday       | The day the appointment was scheduled (datetime).          |
| appointmentday     | The day of the actual appointment (datetime).              |
| age                | Age of the patient (integer).                              |
| neighbourhood      | The neighborhood where the appointment was held.           |
| scholarship        | Indicates whether the patient is enrolled in Bolsa Família (0/1). |
| hipertension       | Whether the patient has hypertension (0/1).                |
| diabetes           | Whether the patient has diabetes (0/1).                    |
| alcoholism         | Whether the patient is an alcoholic (0/1).                 |
| handcap            | Whether the patient is handicapped (0/1).                  |
| sms_received       | Whether the patient received an SMS notification (0/1).    |
| no_show            | Whether the patient showed up for the appointment (`Yes`/`No`). |

---

## 💡 Purpose

This dataset can be used for:

- Predictive modeling: Will a patient miss their appointment?
- Statistical analysis of healthcare behaviors.
- Exploratory Data Analysis (EDA) on social, economic, and health factors.

---

## 💾 Usage

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/your-repo-name.git
    ```

2. Install dependencies (if you’re using Python):
    ```bash
    pip install pandas matplotlib seaborn scikit-learn
    ```

3. Load the dataset:
    ```python
    import pandas as pd
    from google.colab import files
    uploaded = files.upload()
    df = pd.read_csv('medical.csv')
    ```

---

## ⚠️ Notes
we Identify and handle missing values using .isnull() in Python, we can see there are no missing values.
print(df.isnull().sum())
PatientId         0
AppointmentID     0
Gender            0
ScheduledDay      0
AppointmentDay    0
Age               0
Neighbourhood     0
Scholarship       0
Hipertension      0
Diabetes          0
Alcoholism        0
Handcap           0
SMS_received      0
No-show           0
dtype: int64

---
----
we remove duplicate rows using drop_duplicates()
df = df.drop_duplicates()
print(df.shape)

(110527, 14)
There are no duplicates found
----
----
we can Standardize text values 
df['Gender'] = df['Gender'].str.upper()
df['Neighbourhood'] = df['Neighbourhood'].str.title()  
df['No-show'] = df['No-show'].str.upper() 
print(df[['Gender', 'Neighbourhood', 'No-show']].head())

Gender      Neighbourhood No-show
0      F    Jardim Da Penha      NO
1      M    Jardim Da Penha      NO
2      F      Mata Da Praia      NO
3      F  Pontal De Camburi      NO
4      F    Jardim Da Penha      NO
-----
-----
we can convert date formats to a consistent type 
df['ScheduledDay'] = pd.to_datetime(df['ScheduledDay'])
df['AppointmentDay'] = pd.to_datetime(df['AppointmentDay'])
df['ScheduledDay'] = df['ScheduledDay'].dt.strftime('%d-%m-%Y')
df['AppointmentDay'] = df['AppointmentDay'].dt.strftime('%d-%m-%Y')
print(df[['ScheduledDay', 'AppointmentDay','Gender', 'Neighbourhood']].head())

ScheduledDay AppointmentDay Gender      Neighbourhood
0   29-04-2016     29-04-2016      F    Jardim Da Penha
1   29-04-2016     29-04-2016      M    Jardim Da Penha
2   29-04-2016     29-04-2016      F      Mata Da Praia
3   29-04-2016     29-04-2016      F  Pontal De Camburi
4   29-04-2016     29-04-2016      F    Jardim Da Penha
-----
-----
we can rename column headers to be consistent
df.columns = [col.strip().lower().replace(' ', '_') for col in df.columns]
df.columns = [col.replace('-', '') for col in df.columns]
print(df.columns)
Index(['patientid', 'appointmentid', 'gender', 'scheduledday',
       'appointmentday', 'age', 'neighbourhood', 'scholarship', 'hipertension',
       'diabetes', 'alcoholism', 'handcap', 'sms_received', 'noshow'],
      dtype='object')
-----
-----
we can see that to check and fix data types 
scheduledday and appointmentday is in object data type we need to convert it into datetime data type and PatientId is in object data type we need to convert it into float data type.
patientid                float64
appointmentid              int64
gender                    object
scheduledday      datetime64[ns]
appointmentday    datetime64[ns]
age                        int64
neighbourhood             object
scholarship                int64
hipertension               int64
diabetes                   int64
alcoholism                 int64
handcap                    int64
sms_received               int64
noshow                    object
dtype: object
------
