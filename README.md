# Create Looker Custom Visualizations with Gemini (No Coding Required!) 🚀

Looker comes with a great set of standard visualizations, but sometimes you need a chart that fits a very specific business need **or a unique design requirement that goes beyond the built-in library.**

To address this, Looker allows developers to build **Custom Visualizations** to create exactly what is needed. However, while this traditionally requires specialized knowledge of HTML, CSS, and JavaScript, this guide demonstrates how to create them using **Gemini** (Google's Generative AI)—allowing you to build complex custom charts without writing a single line of code yourself.

## 🌟 Examples of What You Can Build
[Advanced Cross Filter](https://github.com/tanakakentarotanaka/looker-viz-library/blob/main/advanced_cross_filtering/README.md)
Creating other samples...



## ⚠️ Prerequisites & Important Notes
Before you start, please note the following:
* **Target Platform:** This guide is for **Looker** (Google Cloud Core/Original), *not* Looker Studio.
* **Permissions:** You need **Developer** permissions or higher.
* **Setup:** Ask your Looker Admin to create a generic **Empty Project** for custom visualizations.
* **Support:** Custom visualizations are not covered by Google's official support.
* **Best Practice:** Always try to use standard visualizations or the [Chart Config Editor](https://cloud.google.com/looker/docs/chart-config-editor) first. Too many custom charts can make dashboards hard to maintain or interpret.

## Dependencies & Licenses
If external libraries are used in your custom visualization, they will be specified in the manifest.lkml file. Please ensure you review and comply with the Terms of Service and License agreements of any external libraries before use.
---

## 🛠️ How to Create It

We will use Gemini to generate the necessary code and instructions.

### Step 1: Generate the Code with Gemini
1.  Open [Gemini](https://gemini.google.com/) (Select a model with "Pro" or higher capabilities).
2.  Copy and paste the **Prompt Template** below into Gemini.
    * *Note: You should customize sections 【1】 and 【2】 based on the chart you want to build.*

#### 🤖 Prompt Template
> **💡 Pro Tip:** Once you are familiar with the process, you don't strictly need to follow this template. Often, simply describing the visualization you want to Gemini in plain language (e.g., *"Make me a bar chart that turns red when values exceed 100"*) is enough to generate working code.
> **🚧 Note on Functionality:** The current prompt template may not fully support advanced features like **Cross-filtering**. I plan to update this repository with improved prompts to handle these features in the future.

```
You are an expert in Looker Custom Visualization development.
Please generate the JavaScript code and setup instructions for a Looker Custom Visualization based on the following requirements.

---
You are an expert in Looker Custom Visualization development.
Please generate the JavaScript code and setup instructions for a Looker Custom Visualization based on the following requirements.

---

### 【1. Overview of the Visualization】
-Modern movement line graph

### 【2. User Configuration Options】
-I want options that are applicable to common anticipated use cases.

### 【3. Output Format & Procedure】
* **Instructions:** Provide a numbered list of steps to set this up in Looker.
* **Code:** Provide the full code for `manifest.lkml` and the `JavaScript` file, ready to copy & paste.
* **For Beginners:** Explain technical terms simply so non-engineers can understand.
* **Language:** Ensure default labels in the code are in English.

### 【4. Technical Requirements】
* **Target Audience:** Users with Looker Developer permissions.
* **File Creation:**
    * `manifest.lkml`: Created via the Looker IDE "+" button.
    * JavaScript file: Created locally and dragged & dropped into the Looker IDE.
* **`manifest.lkml` details:**
    * Do not include the `project_name` parameter.
    * Ensure the `visualization` id is unique.
    * Example:Replace the placeholder values (id, label, file) with descriptive names relevant to the visualization
        ```lkml
        visualization: {
          id: "unique-id-name"
          label: "My Custom Chart"
          file: "sample.js"
          dependencies: ["[https://d3js.org/d3.v7.min.js](https://d3js.org/d3.v7.min.js)"]
        }
        ```
* **JavaScript details:**
    * Use `looker.plugins.visualizations.add`.
    * Provide code that works standalone and is stable.
    * If external libraries (like D3.js) are needed, load them via the `dependencies` parameter from a reliable CDN.

* **Critical: Cross-filtering Implementation (Strict Adherence to API V2):**
    * **Render Function:** MUST use `updateAsync` (not `update`) and call the `done()` callback when rendering is finished.
    * **Event Handling:** * When a data element is clicked, check if `details.crossfilterEnabled` is true.
        * If true, trigger `LookerCharts.Utils.toggleCrossfilter({row: d.row, event: event})`.
    * **Visual State & Styling:** * Use `LookerCharts.Utils.getCrossfilterSelection(row, pivot)` to determine the selection state of each element.
        * The function returns: `0` (None/Normal), `1` (Selected), `2` (Unselected/Background).
        * **Logic:** If the state is `2` (Unselected), strictly reduce opacity (e.g., 0.2) or gray out the element to visually highlight the selected items.
```

### Step 2: Implement in Looker
Follow the instructions generated by Gemini. The general flow is as follows:

1.  **Open the Project:** Go to the empty project created by your admin.
2.  **Create Manifest:**
    * Click the `+` icon in the file browser -> **Create Project Manifest**.
    * Paste the `manifest.lkml` code provided by Gemini.
    * Click **Save Changes**.
3.  **Create JS File:**
    * Open a text editor (Notepad, TextEdit, VS Code) on your computer.
    * Paste the JavaScript code provided by Gemini.
    * Save the file (e.g., `my_custom_chart.js`).
4.  **Upload:** Drag and drop your JS file into the Looker IDE file browser.
5.  **Commit & Deploy:**
    * Click **Validate LookML**.
    * Click **Commit Changes & Push**.
    * **Crucial Step:** Click **Deploy to Production**.
    * *Note: Custom visualizations often require deployment to production to render correctly during testing.*

### Step 3: Verify in an Explore
1.  Open any Explore in Looker.
2.  In the Visualization bar, click `...`.
3.  You should see your new custom chart listed! Select it and test the configuration options.

---

## Troubleshooting & Customization Tips

If you encounter errors or wish to add new features, please remember that **working with AI is an iterative process**.

* **🔄 Multi-turn & Persistence (Important):**
    Whether fixing a bug or adding a feature, a single prompt is rarely enough. It is crucial to engage in a **multi-turn conversation (back-and-forth dialogue)** with the AI. If the AI gets confused or the code becomes messy, **don't hesitate to reset the chat** and try asking again from scratch.
* **Paste Errors to Gemini:** Copy any error messages or describe the unexpected behavior to Gemini.
* **Share Your Code:** Paste your current `manifest.lkml` and JS code back to Gemini so it can check for syntax errors.
* **Screenshots:** Sometimes showing Gemini a screenshot of the issue works better than text explanations.

## 🧪 Testing & Maintenance
* **Ask Gemini for Test Cases:** Ask, "How should I test this chart to ensure it's robust?" Gemini can suggest boundary tests (min/max values) and irregular inputs.
* **Updates:** To change the design (e.g., "Make the bars red"), simply ask Gemini to modify the code.

---
---

### Reference Source
https://github.com/looker/custom_visualizations_v2/blob/master/docs/api_reference.md#api-20-reference

### 📝 Author & Copyright
This content is an English translation of the original article:
[【Looker】非エンジニアでもOK！Geminiで自由にオリジナルのグラフ...](https://zenn.dev/google_cloud_jp/articles/48159e8495944d)

*This translation is provided by the original author themselves, and the copyright belongs to the author.*
