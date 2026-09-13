# 🖼️ Doing More with Maps — Custom Backgrounds

Welcome back!

In addition to traditional geographic maps, **Tableau** allows you to create **custom maps** using your own background images.

These custom maps enable you to visualize data on floor plans, production layouts, diagrams, and many other non-geographic images.

---

# 🎯 Spatial Visualization Beyond Geographic Maps

Not all spatial data belongs on a world map.

Sometimes, a simplified or symbolic representation communicates information more effectively.

Examples include:

- 🚇 Metro or subway maps
- 🏭 Factory production line layouts
- 🏠 Home floor plans
- 🛣️ Road trip route maps
- 🖼️ Museum layouts
- 🏢 Office seating plans

These custom maps help users quickly understand locations and movement without the complexity of real-world geography.

---

# 📍 Coordinates: Latitude & Longitude vs. X & Y

Every map requires a coordinate system.

## 🌍 Geographic Maps

Use:

- 📍 Latitude
- 📍 Longitude

These coordinates identify real-world locations.

---

## 🖼️ Custom Maps

Custom backgrounds use:

- ➡️ X coordinate
- ⬆️ Y coordinate

Every pixel within a 2D image can be identified using X and Y coordinates.

To plot objects on a custom background, you must know the X and Y position of each point of interest.

---

# 📌 Point and Polygon Custom Maps

As with geographic maps, custom maps can use different geometry types.

## 📍 Point Maps

Point maps identify specific locations.

Examples include:

- 🚪 Rooms
- 🖥️ Workstations
- 🖼️ Museum exhibits
- ⚙️ Machines

Point maps require relatively little data and are ideal for pinpointing exact locations.

---

## 🔷 Polygon Maps

Polygon maps represent entire areas rather than individual points.

Examples include:

- 🏢 Office departments
- 🏠 Rooms
- 🏭 Factory zones
- 🖼️ Exhibition halls

Polygons provide more detailed boundaries but require more coordinate data than point maps.

---

# ✨ Enriching Custom Maps

Both point and polygon maps can be enhanced with additional information.

Examples include:

- 👥 Occupancy
- ⚡ Electricity usage
- 🏭 Machine status
- 🚨 Production failures
- 📈 Visitor traffic
- 📊 Performance metrics

This transforms a simple image into an interactive analytical dashboard.

---

# 🛠️ Steps for Creating a Custom Map

Creating a custom map in Tableau typically involves the following process.

## 1️⃣ Upload a Background Image

Choose the image that represents your layout, such as:

- 🏠 Floor plan
- 🏭 Factory layout
- 🖼️ Museum map
- 🚇 Transit map

---

## 2️⃣ Identify Coordinates

Unlike geographic maps, Tableau cannot automatically determine locations.

You must manually identify the:

- ➡️ X coordinates
- ⬆️ Y coordinates

for each point or polygon on the image.

---

## 3️⃣ Create a Location Dataset

Store the coordinate information in a dataset.

Typical fields include:

- 📍 Location name
- ➡️ X coordinate
- ⬆️ Y coordinate

---

## 4️⃣ Combine Additional Data

Join the coordinate dataset with other business data.

Examples include:

- 👥 Room occupants
- ⚡ Electricity consumption
- 🕒 Time of day
- 🏭 Equipment status
- 📈 Visitor counts

---

## 5️⃣ Visualize the Data

Build interactive visualizations using:

- 🎨 Colors
- 📏 Sizes
- 🏷️ Labels
- ✨ Animations (when appropriate)

The result is an informative custom map that supports exploration and analysis.

---

# 🏛️ Museum Visits Dataset

In the upcoming exercises, you'll work with a **museum floor plan**.

Using the custom background, you'll analyze:

- 👣 Visitor traffic
- 🕒 Changes throughout the day
- 🚶 Common visitor paths
- 🖼️ Popular exhibition areas

This demonstrates how custom maps can reveal movement patterns in non-geographic environments.

---

# 📚 Key Terms

| 📖 Term | 📝 Description |
|----------|----------------|
| 🖼️ Custom Map | A visualization built on a user-provided background image |
| 📍 Point Map | Displays specific locations using X and Y coordinates |
| 🔷 Polygon Map | Represents areas using enclosed shapes |
| ➡️ X Coordinate | Horizontal position on a custom image |
| ⬆️ Y Coordinate | Vertical position on a custom image |
| 🗂️ Location Dataset | Dataset containing coordinates for plotting objects |

---

# ✅ Key Takeaways

- 🖼️ Tableau supports mapping on custom background images in addition to geographic maps.
- 📍 Custom maps rely on **X and Y coordinates** instead of latitude and longitude.
- 🔷 Both point and polygon geometries can be used on custom backgrounds.
- 📊 Additional datasets can be combined with coordinates to create rich, interactive visualizations.
- 🏛️ The chapter uses a museum floor plan to analyze visitor movement and traffic patterns.

---

# 🚀 Let's Practice!

Now it's time to test your understanding before creating custom maps and interactive spatial visualizations in Tableau.
