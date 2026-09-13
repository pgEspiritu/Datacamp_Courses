# 📊 Tableau Interface & Data Roles

---

## 1. Tableau Interface 🖥️  
This is the interface for Tableau worksheets, where you will create your visualizations.

It contains several components that work together to help you build dashboards.

We’ll explore them in practice, but first we need to understand key Tableau terms (jargon).

---

## 2. Data Pane 📁  
The **Data Pane** shows the data sources you have loaded.

Example:
- 📄 Airbnb listings in San Francisco (single dataset)

You will also see another tab:
- 🧠 Analytics pane (covered later in the course)

---

## 3. Fields in the Data Pane 📊  
The data pane shows all available fields (columns) from your dataset.

You will notice two key visual differences:
- 🟢 Green fields
- 🔵 Blue fields

---

## 4. Continuous Fields 🟢  
Green fields are **continuous fields**.

They represent:
- 📈 Infinite ranges of values  
- Numeric or measurable scales  

### Examples:
- Reviews per month  
- Room price  
- Longitude  

---

## 5. Discrete Fields 🔵  
Blue fields are **discrete fields**.

They represent:
- 🧾 Separate, distinct values  
- Categories or identifiers  

### Examples:
- Room type  
- Neighborhood  
- Listing ID  

---

## 6. Dimensions 📂  
Dimensions appear at the **top of the data pane**.

They contain **qualitative data**, such as:
- 🏷️ Names  
- 📅 Dates  
- 🏘️ Categories  

### Examples:
- Neighborhood  
- Room Type  
- Reviews per month (if treated as a category)

---

## 7. Measures 📏  
Measures appear under Dimensions.

They contain **quantitative numeric data** that can be:
- ➕ Aggregated  
- 📊 Measured  

### Examples:
- 💰 Price  
- 🛏️ Minimum nights  
- ⭐ Total reviews  

👉 Tableau automatically assigns these roles, but you should always review them.

---

## 8. Converting Data Roles 🔄  
You can convert fields between:
- 📂 Dimensions ↔ 📏 Measures  
- 🔵 Discrete ↔ 🟢 Continuous  

### Example:
- Reviews per month can be converted into a **measure** to calculate averages

---

## 9. Data Role Combinations 📚  
### Common combinations:
- 🔵 Discrete Dimensions (e.g., eye color, gender)
- 🟢 Continuous Measures (e.g., height, weight)

### Less common combinations:
- 🔵 Discrete Measures (e.g., shoe size, age)
- 🟢 Continuous Dimensions (e.g., date)

---

## 10. Why Data Roles Matter ⚠️  
Data roles affect how you build visualizations.

- 📂 Dimensions → group and segment data  
- 📏 Measures → aggregate and calculate values  

### Example:
- Calculate average price per room type

👉 This is called **segmentation**

---

## 11. Building Visualizations 🧱  
Visualizations are created using **drag and drop**:
- 📂 Dimensions
- 📏 Measures

You drop them onto:
- Canvas
- Shelves
- Cards

---

## 12. Canvas 🎨  
The **Canvas** is where your visualization appears.

---

## 13. Columns & Rows 📐  
- 📊 Columns → X-axis  
- 📊 Rows → Y-axis  

These define how your chart is structured.

---

## 14. Pages 📄  
The Pages shelf lets you split visualizations into multiple views.

### Example:
- One page per neighborhood

---

## 15. Filters 🎛️  
The Filters shelf allows you to:
- 🔍 Include or exclude data  
- 🎯 Focus on specific subsets  

(Will be covered in detail later)

---

## 16. Marks 🎯  
The Marks area controls how data is displayed.

It includes:
- Marks card  
- Marks type  

---

## 17. Marks Cards 🎨  
Marks cards control:
- 🎨 Color  
- 📏 Size  
- 🔷 Shape  

These add context and detail to your visualization.

---

## 18. Marks Types 🔘  
Marks type determines how data is displayed:
- Bar chart  
- Line chart  
- Map  
- Scatter plot  

You can change it depending on your analysis needs.

---

## 19. Toolbar 🛠️  
The toolbar provides quick actions:
- ↩️ Undo  
- ↪️ Redo  
- 🔃 Sort  
- 🧹 Clear canvas  

---

## 20. Business Question 🏙️  
Now it’s time to apply what you learned.

You will explore:
📊 Room prices across New York neighborhoods  

---

## 21. Let’s Practice! 🧠  
Before moving forward, test your understanding of:
- Dimensions 📂  
- Measures 📏  
