# 🗺️ Visualizing Data on Geographical Maps

Welcome!

In this chapter, you'll learn how to create **maps in Tableau**, covering both:

- 🌍 Traditional geographical maps
- 🎨 Custom maps using your own backgrounds

Mapping is one of Tableau's most powerful visualization capabilities, allowing you to uncover geographic patterns and location-based insights.

---

# 🌎 The World of Digital Cartography

**Cartography** is the science and art of creating maps.

Modern **digital cartography** has transformed traditional paper maps into interactive digital experiences.

Examples include:

- 🛰️ Google Maps with 3D visualization
- 📍 GPS navigation systems
- 🌐 Interactive online mapping applications

A major technology behind digital mapping is the **Geographic Information System (GIS)**, which organizes, analyzes, and visualizes spatial data.

As GIS has evolved, new careers have emerged, including:

- 👨‍💻 GIS application developers
- 📊 Location intelligence specialists
- 🗺️ GIS analysts

---

# 📐 Basic Digital Geometries

Spatial data is built from three fundamental geometry types.

## 📍 Point

A **point** represents a specific location.

It is defined by:

- X coordinate (Longitude)
- Y coordinate (Latitude)

In 3D maps, a point may also include:

- Z coordinate (Elevation)

### Example

- 📍 City location
- 🏠 Building
- 🛫 Airport

---

## 📏 Line

A **line** connects multiple points together.

It is often used to represent:

- 🛣️ Roads
- 🚆 Railways
- 🌊 Rivers
- ✈️ Flight routes

A sequence of connected lines is sometimes called a **polygonal chain**.

---

## 🔷 Polygon

A **polygon** is a closed shape created by connecting multiple lines.

Examples include:

- 🏙️ City boundaries
- 🌍 Countries
- 🏘️ Neighborhoods
- 📍 Administrative regions

Polygons are commonly used to visualize regions and areas on maps.

---

# 🌍 Types of Geographic Data

Tableau supports multiple forms of geographic information.

## 📄 Text and Spreadsheet Data

These files may contain:

- 🌎 Country names
- 🏙️ City names
- 📍 Latitude
- 📍 Longitude
- ✈️ Airport codes
- 📊 Statistical region codes (such as **NUTS**)

These datasets are commonly used to create **point maps**.

---

## 🗂️ Spatial Files

Tableau also supports specialized spatial file formats, including:

- 🗺️ Shapefile (.shp)
- 📦 GeoJSON (.geojson)

These files contain the coordinate information necessary to draw:

- 📍 Points
- 📏 Lines
- 🔷 Polygons

They often include additional metadata describing geographic features.

---

# 🌐 Recognizing Geographic Fields in Tableau

When geographic data is imported, Tableau often recognizes location fields automatically.

Recognized geographic fields display a:

🌍 **Globe icon**

When Tableau recognizes a location, it automatically generates:

- 📍 Latitude
- 📍 Longitude

These fields allow Tableau to position locations accurately on a map.

---

## ✋ Manual Geographic Roles

Sometimes Tableau cannot recognize geographic information automatically.

In these cases, you may need to:

- 🔢 Convert latitude and longitude into numeric values
- ✍️ Correct spelling mistakes
- 🌍 Assign the correct **Geographic Role**
- 📂 Upload a custom geocoding file

### Example

If you're mapping:

- 🏫 Schools
- 🎓 Universities

You may need to provide a dataset containing their latitude and longitude coordinates.

---

# 📦 Working with GeoJSON

**GeoJSON** is a popular format for storing geographic data.

It can represent:

- 📍 Points
- 📏 Lines
- 🔷 Polygons
- 🧩 Multipolygons

For example, a GeoJSON file can describe city neighborhoods or administrative districts.

### Example

A map of **Amsterdam's neighborhoods** may include districts represented as **multipolygons**, where one region consists of multiple connected polygon shapes.

GeoJSON files are editable and can be customized to suit different mapping needs.

Helpful editor:

🌐 https://geojson.io/

---

# 🏠 Airbnb Dataset

Throughout this chapter, you'll explore an **Airbnb** dataset focused on **Barcelona**.

Using Tableau maps, you'll analyze geographic insights such as:

- 🏘️ Airbnb listing locations
- 🌆 Popular tourist areas
- 📊 Spatial patterns
- 🗺️ Interactive geographic visualizations

Dataset source:

🌐 http://insideairbnb.com/barcelona

---

# 📚 Key Terms

| 📖 Term | 📝 Description |
|----------|----------------|
| 🗺️ Cartography | The science and art of creating maps |
| 🌍 GIS | Geographic Information System used for managing and analyzing spatial data |
| 📍 Point | A single geographic location |
| 📏 Line | A path connecting multiple points |
| 🔷 Polygon | A closed geographic area or boundary |
| 📦 GeoJSON | A file format for storing geographic data |
| 🌎 Geographic Role | Tableau's designation for location fields |
| 📍 Latitude & Longitude | Coordinates used to position locations on maps |

---

# ✅ Key Takeaways

- 🗺️ Tableau supports both standard geographic maps and custom spatial maps.
- 📍 Geographic data can be stored as coordinates, location names, or spatial files.
- 🌍 Tableau automatically recognizes many geographic fields and creates latitude and longitude values.
- 📦 GeoJSON files can represent complex spatial objects like points, lines, polygons, and multipolygons.
- 🏠 The chapter uses Airbnb data from Barcelona to demonstrate interactive geographic analysis.

---

# 🚀 Let's Practice!

Now it's time to test your understanding before building interactive maps in Tableau.
