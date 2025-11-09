# 🧹 Customer Call List Data Cleaning using Python (Pandas)

This project demonstrates how to clean and preprocess a **Customer Call List** dataset using **Python** and **Pandas**. The goal is to make the dataset ready for analysis by removing duplicates, cleaning phone numbers, fixing inconsistent values, and handling missing data — and finally saving the cleaned file as a CSV.

---

## 🚀 Key Features

- Remove duplicate records  
- Drop unnecessary columns  
- Clean and standardize `Last_Name` values  
- Format phone numbers (e.g. `123-456-7890`)  
- Split address into `Street`, `Country`, and `Zip`  
- Convert “Yes/No” to “Y/N” for uniformity  
- Handle missing and invalid data  
- Export cleaned dataset to a **CSV file**

---


import pandas as pd
df = pd.read_excel("Customer Call List.xlsx")
df.head()
df
df.drop_duplicates(inplace=True)
df
df.drop(columns="Not_Useful_Column",inplace=True)
df
df.drop(columns="Not_Useful_Column",inplace=True)
df
df["Last_Name"]=df["Last_Name"].str.strip("/")
df
df["Last_Name"]=df["Last_Name"].str.strip("._")
df
df["Phone_Number"] = df["Phone_Number"].astype(str).str.replace(r"\D", "", regex=True)
df["Phone_Number"] = df["Phone_Number"].apply(
    lambda x: f"{x[0:3]}-{x[3:6]}-{x[6:10]}" if len(x) == 10 else x
)
df
df[['Street', 'Country', 'Zip']] = df['Address'].str.split(pat=',', n=2, expand=True)
df
df["Paying Customer"]= df["Paying Customer"].str.replace("Yes","Y")
df["Paying Customer"]= df["Paying Customer"].str.replace("No","N")
df["Do_Not_Contact"]= df["Do_Not_Contact"].str.replace("Yes","Y")
df["Do_Not_Contact"]= df["Do_Not_Contact"].str.replace("No","N")
df
df = df.replace("N/a","")
df
df = df.fillna("")
df
df = df.drop(columns="Address")
df
df.to_csv("Cleaned_customer_data.csv",index=False)

