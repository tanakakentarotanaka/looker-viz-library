# Advanced Cross Filter (Custom Visualization)

This is a Custom Visualization for Looker that functions as an interactive filter. **Unlike standard filters, it allows for free placement anywhere on the dashboard and triggers instant updates without requiring an update button.**

<img width="800"  alt="Image" src="https://github.com/user-attachments/assets/22b6ad9c-7e4e-4e6d-a599-9315d25bd187" />

(There is a Gemini mark on the image, but I just used Gemini to white out the image. Apart from this editing, it is the actual screen.)

> **Demo Video:** [Watch on YouTube](https://www.youtube.com/watch?v=yk9xEDG_5Lw)


## Overview
This component allows you to filter dashboard data interactively via a visualization tile. Unlike standard filters, it supports immediate updates and rich styling.

*Note: Parts of this code were generated using Gemini. As a custom visualization, this is not officially supported by Looker/Google. Please use at your own risk.*

## Key Features (Pros)

### 🚀 Instant Interaction
**No need to press an "Update" button.**
Filtering is applied immediately upon selection, providing a seamless user experience.
![Instant Interaction](https://scrapbox.io/files/691c33ce0c61ad8d6950c2ea.png)

### 🎨 Flexible Layout
**Place it anywhere.**
Since this acts as a visualization tile, you can position it anywhere on your dashboard layout. cf.Standard filters are restricted to the top or right side of the dashboard.
![Layout](https://scrapbox.io/files/6921c9f13e863830990ebf16.png)

### 📊 Integrated Data Visualization
**Visualize Measures.**
You can display measures alongside your filter dimensions using data bars and color scales, giving context to the filter options.
![Data Bars](https://scrapbox.io/files/691c36ecb813ed3efbf136d2.png)

### 🖌️ Granular Design Control
Customize backgrounds, transparency levels, and even use images as backgrounds for a highly polished look.
![Design](https://scrapbox.io/files/6921cea2bfa9b6c6e9d5ea89.png)

## Limitations & Considerations (Cons)

* **Query Cost / Performance:**
    * **Increased Query Volume:** Because of the cross-filtering nature, clicking a tile immediately triggers a query. This ease of use can lead to higher query counts compared to standard filters where users batch selections before updating.
    * **Sequential Processing:** When selecting multiple items, filters are applied one by one (sequential queries) rather than processing a batch of selections at once.
* **Functional Differences:**
    * Some complex logic available in standard filters (e.g., relative date logic like "Today") is not currently supported.
    * *Supported Logic:* Partial match, Exclude, Number range, and Regex search are implemented.
    ![Search Logic](https://scrapbox.io/files/691c382fb0ceba5ef2f7d9a9.png)

## Data Requirements

* **Dimension:** 1 Field (Required)
* **Measure:** Optional (For data bars and color scale)

## Disclaimer
This is a custom visualization sample. If you require additional features, you may try modifying the code using AI tools like Gemini. Support is not provided for this visualization.

---
