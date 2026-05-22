# task11import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# ==============================
# STEP 1: CREATE DATASET
# ==============================

data = {
    "Student": ["A","B","C","D","E","F","G","H"],
    "Study_Hours": [5,2,7,4,6,3,8,5],
    "Phone_Hours": [3,6,2,5,4,7,1,3],
    "Sleep_Hours": [7,5,8,6,7,5,8,6],
    "Social_Media": [2,4,1,3,2,5,1,2],
    "Marks": [75,50,85,65,78,55,90,70]
}

df = pd.DataFrame(data)

# Save dataset
df.to_csv("student_data.csv", index=False)

print("\n✅ Original Data:\n", df)


# ==============================
# STEP 2: DATA CLEANING
# ==============================

print("\n🔍 Checking Missing Values:\n", df.isnull().sum())

# Fill missing values
df.fillna(df.mean(numeric_only=True), inplace=True)

# Remove duplicates
df.drop_duplicates(inplace=True)

# Remove outliers (basic filtering)
df = df[(df['Study_Hours'] <= 12) & (df['Phone_Hours'] <= 12)]

print("\n✅ Cleaned Data:\n", df)


# ==============================
# STEP 3: BASIC ANALYSIS
# ==============================

print("\n📊 Statistical Summary:\n", df.describe())

print("\n📌 Correlation:\n", df.corr(numeric_only=True))


# ==============================
# STEP 4: VISUALIZATION
# ==============================

sns.set(style="whitegrid")

# 1. Study Hours vs Marks
plt.figure()
sns.scatterplot(x='Study_Hours', y='Marks', data=df)
plt.title("Study Hours vs Marks")
plt.savefig("study_vs_marks.png")
plt.show()

# 2. Phone Usage vs Marks
plt.figure()
sns.scatterplot(x='Phone_Hours', y='Marks', data=df, color='red')
plt.title("Phone Usage vs Marks")
plt.savefig("phone_vs_marks.png")
plt.show()

# 3. Sleep vs Marks
plt.figure()
sns.barplot(x='Sleep_Hours', y='Marks', data=df)
plt.title("Sleep Hours vs Marks")
plt.savefig("sleep_vs_marks.png")
plt.show()

# 4. Correlation Heatmap
plt.figure()
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.title("Correlation Matrix")
plt.savefig("correlation.png")
plt.show()

# 5. Pairplot (Advanced)
sns.pairplot(df)
plt.savefig("pairplot.png")
plt.show()


# ==============================
# STEP 5: INSIGHTS (PRINT)
# ==============================

print("\n🧠 INSIGHTS:")
print("- Students who study more tend to score higher.")
print("- Higher phone usage negatively affects marks.")
print("- Proper sleep improves academic performance.")
