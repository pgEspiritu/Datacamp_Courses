# 🗺️ Mapping Your Data in Tableau

---

## 1. Mapping Your Data 🌍  
Welcome to **Chapter 3**!

In this chapter, you'll create more advanced visualizations and learn how Tableau can use **geographic data** to build interactive maps.

---

## 2. What is Geographic Data? 🗺️

Geographic data refers to information associated with specific locations on Earth.

### 📌 Examples:
- 🌎 Countries around the world
- ✈️ Flight paths between regions
- 🛢️ Oil pipeline networks
- 🏙️ Cities and provinces
- 📮 Postal code areas

Visualizing this data on maps helps users:
- Identify patterns
- Understand regional differences
- Make better decisions

---

## 3. Types of Maps in Tableau 🗺️

Tableau supports two primary map types:

### 🎨 Filled Maps
A **Filled Map** displays geographic boundaries filled with colors.

#### Characteristics:
- Colors represent values or categories
- Regions are shaded based on data
- Useful for comparing areas

### Example:
- Different U.S. states colored according to population, sales, or health indicators

---

## 4. Symbol Maps 📍

A **Symbol Map** uses symbols to represent geographic locations.

### Characteristics:
- Places a symbol at the center of a geographic region
- Symbol size, color, or shape can represent data values
- Excellent for showing individual locations

### Example:
- A circle placed in the center of each U.S. state
- Circle size may represent population
- Circle color may represent a health metric

📌 This lesson focuses on creating **Symbol Maps**.

---

## 5. Recognized Geographic Types 🌐

Tableau includes a powerful internal geographic database.

It can automatically recognize many geographic data types.

### Supported Geographic Types:
- ☎️ U.S. Area Codes
- 🏙️ Cities Worldwide
- 🏛️ U.S. Congressional Districts
- 🌎 Countries and Regions Worldwide
- 🏘️ U.S. Counties
- 🗺️ States and Provinces Worldwide
- 📮 Postal Codes

---

## 6. Geocoding 📌

When Tableau recognizes a geographic field, it automatically assigns geographic coordinates (latitude and longitude).

This process is called:

### 🌍 Geocoding

**Geocoding** = Converting place names into map coordinates.

### Examples:
| Geographic Value | Coordinates Assigned |
|------------------|---------------------|
| Philippines | Latitude & Longitude |
| New York | Latitude & Longitude |
| Tokyo | Latitude & Longitude |

---

## 7. Globe Icon 🌐

In Tableau, geocoded fields are easy to identify.

### Indicator:
🌐 **Globe Icon**

If a field displays a globe icon, Tableau recognizes it as geographic data and can map it automatically.

---

## 8. Dataset Used 📊🌍

In this chapter, you will work with:

- 🌍 Gapminder Dataset
- 🇺🇳 United Nations Dataset

The datasets contain worldwide health-related statistics.

---

## 9. Business Context 🏥

Imagine you are working for the:

🏥 :contentReference[oaicite:0]{index=0}

Your task is to analyze historical health and population data.

### Why?
Understanding historical trends helps support decisions about:

- 🌍 International health programs
- 🚑 Public health initiatives
- 📈 Population management
- 🏥 Health risk reduction

within the:

🇺🇳 :contentReference[oaicite:1]{index=1} system.

---

## 10. Business Question ❓

At the end of this lesson, you will answer:

> **What was the population growth of the country with the highest population in 2008?**

### Why is this important?
Understanding population growth helps the World Health Organization:

- 📈 Identify rapidly growing populations
- ⚠️ Assess risks related to overpopulation
- 🏥 Allocate health resources effectively
- 🌍 Improve global health planning

---

## 11. Demo Time! 🎬

Now it's time to learn how to create a **Symbol Map** in Tableau and visualize geographic data effectively.
