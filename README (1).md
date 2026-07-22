
# 📊 Online Courses Analytics Dashboard | Power BI Project

## 📌 Project Overview
This project focuses on analyzing **online recorded courses data** for an **EdTech startup** aiming to expand and optimize its course offerings. The client collected raw data from multiple EdTech platforms but required structured analysis to uncover insights related to **course demand, viewer engagement, instructor performance, and content accessibility**.

Using **Power BI**, I performed end-to-end **data cleaning, transformation, modeling, and visualization** to build an interactive dashboard that supports data-driven decision-making.

---

## 🎯 Business Problem
The client wanted to:
- Understand **which categories and course types perform best**
- Identify **learner preferences** across languages, duration, and subtitles
- Discover **top-performing instructors**
- Optimize content strategy for **maximum engagement and growth**

---

## 📂 Dataset Information
- **Source**: Aggregated data from various EdTech platforms  
- **Format**: CSV  
- **Key Columns**:
  - Course ID
  - Category & Sub-Category
  - Course Type
  - Language
  - Number of Viewers
  - Ratings
  - Instructor(s)
  - Course Duration
  - Subtitle Languages

> ⚠️ Raw data contained duplicates, blank rows, empty columns, inconsistent text formats, and mixed data types.

---

## 🧹 Data Cleaning & Transformation (Power Query)
The following transformations were applied:

- Removed **duplicate rows, blank rows, and error values**
- Dropped **100% empty columns** and **URL columns** (irrelevant for analysis)
- Cleaned **Ratings column**:
  - Extracted numeric value from text like `4.9 stars`
  - Converted to **decimal datatype**
- Cleaned **Subtitle column**:
  - Removed prefix text such as `Subtitles:`
- Standardized **Instructor column**:
  - Split multiple instructors per course
  - Unpivoted data to have **one instructor per row**
- Converted **Course Duration** into **hours**:
  - Months → `months × 60 hours`
  - Hours → direct numeric value
  - Minutes → `minutes / 60`
  - Flexible schedules → defaulted to `200 hours`

```m
if Text.Contains(Text.Lower([Duration]), "months") then
    Number.FromText(Text.Select([Duration], {"0".."9"})) * 60
else if Text.Contains(Text.Lower([Duration]), "hours") then
    Number.FromText(Text.Select([Duration], {"0".."9"}))
else if Text.Contains(Text.Lower([Duration]), "minute") then
    Number.FromText(Text.Select([Duration], {"0".."9"})) / 60
else
    200
````

---

## 📊 Business Requirements & Analysis Performed

### 1️⃣ Course Distribution Analysis

* Analyzed **course types across categories**
* Counted number of courses by **category and sub-category**
* 📈 Visual: Bar chart (Course Type vs Count)

---

### 2️⃣ Viewer Engagement Analysis

* Calculated **average number of views** by:

  * Category
  * Sub-category
  * Language
* Used **drill-down** for deeper insights
* 📈 Visual: Bar chart with slicers

---

### 3️⃣ Language Distribution

* Analyzed the distribution of courses across different languages
* 📊 Visual: Pie chart (Language vs Course Count)

---

### 4️⃣ Top 5 Categories by Viewer Preference

* Identified **top 5 categories** based on average viewership
* Analyzed **language preferences** within these categories
* 📐 DAX Logic:

```DAX
Average number of views =
IF(
    RANKX(
        ALL(Online_Courses[Category]),
        CALCULATE(AVERAGE(Online_Courses[Number of viewers]))
    ) < 6,
    CALCULATE(AVERAGE(Online_Courses[Number of viewers])),
    BLANK()
)
```

---

### 5️⃣ Impact of Subtitles on Viewership

* Created a column to calculate **number of subtitles per course**

```m
List.Count(Text.Split([Subtitle Languages], ","))
```

* Analyzed relationship between **subtitles and views**
* 📈 Visual: Line chart

---

### 6️⃣ Top 3 Instructors by Ratings (Static View)

* Identified **top instructors per category & sub-category**
* Ranked instructors based on **average ratings**
* 📐 DAX Measure:

```DAX
Instructor_rating =
IF(
    RANKX(
        ALL(Teachers[Name]),
        CALCULATE(AVERAGE(Teachers[Rating]))
    ) <= 3,
    CALCULATE(AVERAGE(Teachers[Rating])),
    BLANK()
)
```

* 📊 Visual: Table (static Top 3 instructors)

---

### 7️⃣ Course Duration vs Viewer Engagement

* Studied how **course length impacts viewership**
* Analyzed trends across **categories and sub-categories**
* 📈 Visual: Line chart (Duration vs Views)

---

## 🖥️ Dashboard Features

* Category-wise slicers
* Drill-down & drill-through enabled visuals
* Static and dynamic ranking visuals
* Optimized for **business storytelling and decision-making**

---

## 🛠️ Tools & Technologies Used

* **Power BI**
* **Power Query (M Language)**
* **DAX**
* Data Modeling
* Interactive Dashboard Design

---

## 📌 Key Insights

* Certain categories consistently outperform others in engagement
* Language preference varies significantly by category
* Subtitles positively influence viewer engagement
* Short-to-medium duration courses attract higher views
* A small group of instructors consistently deliver high-rated content

---

## 📎 Conclusion

This project demonstrates how **raw, unstructured data** can be transformed into a **business-ready analytics dashboard**. The insights generated help the EdTech startup make informed decisions about **content strategy, instructor partnerships, and learner accessibility**.

---

## 📬 Connect With Me

If you’d like to discuss this project or collaborate on analytics challenges:

* **LinkedIn**: *www.linkedin.com/in/mandar-manjare*
* **Email**: *mandar.manjare07@gmail.com*

⭐ If you found this project useful, feel free to star the repository!

```

---

