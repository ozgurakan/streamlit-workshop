Whether you're learning Streamlit or demonstrating its simplicity to others, this workshop provides a hands-on introduction you can deliver. Feel free to use it.

## Streamlit Workshop Curriculum & Materials

- Workshop Title: Get Started with Interactive Web Apps: A 2-Hour Streamlit Workshop
- Target Audience: Beginners with a basic understanding of Python. No web development experience is required.
- Learning Objectives:
    * Install and run a Streamlit application.
    * Understand the core components of a Streamlit app.
    * Use Streamlit functions to display text, data, and visualizations.
    * Incorporate interactive widgets for user input.
    * Build and deploy a simple, interactive data exploration application.

## Workshop Timeline Overview

| **Section** | **Time** | **Activities** |
|-------------|----------|----------------|
| **Part 1: Introduction & Quick Start** | 20 mins | Setup, first app |
| **Part 2: Streamlit Fundamentals** | 50 mins | Text, widgets, charts |
| **Part 3: Final Project** | 40 mins | Build complete dashboard |
| **Part 4: Share & Next Steps** | 20 mins | Deployment, resources |
| **Buffer/Q&A** | 10 mins | Questions, troubleshooting |
| **Total** | **140 mins (2h 20m)** | |

> **Presenter Tip:** Build in natural 5-10 minute breaks during longer sections

## Troubleshooting Guide

### Common Setup Issues
- **Codespaces not loading**: Share backup environment or switch to local setup
- **Port forwarding problems**: Use VS Code "Ports" tab to manually forward port 8501
- **Package installation fails**: Check Python version, try `pip install --upgrade pip`

### Runtime Problems  
- **App won't start**: Check for syntax errors, missing imports
- **Widgets not working**: Ensure proper indentation, check for typos
- **Charts not displaying**: Verify matplotlib backend, try `st.pyplot(fig, clear_figure=True)`

### Presenter Notes
- **Keep energy high** - Streamlit is exciting, let that show!
- **Code along approach** - Don't just lecture, have everyone build together
- **Celebrate small wins** - Each working app is an achievement
- **Time management** - Use "parking lot" for advanced questions
- **Have backups ready** - Pre-built apps, sample code, screenshots


## Part 1: Introduction & Quick Start (20 minutes)

### 1.1: Welcome and Introduction (5 mins)

**(Presenter's Talking Points)**

* "Welcome everyone! In the next two hours, we're going to learn how to build and share interactive web applications entirely in Python using a fantastic library called Streamlit."
* "Have you ever done a data analysis in a Jupyter Notebook and wished you could easily turn it into a user-friendly tool for others to use? That's the problem Streamlit solves."
*   "Streamlit is an open-source Python library that lets you create web apps for data science and machine learning projects with incredible speed. You don't need to know any HTML, CSS, or JavaScript. If you can write a Python script, you can build a Streamlit app."
* "By the end of this session, you will have built your own interactive data dashboard and will know how to share it with the world."

### 1.2: Environment Setup (10 mins)

**We'll use GitHub Codespaces for the best experience** - it provides a complete development environment in your browser with automatic port forwarding.


**Quick Setup Steps:**

1. **Create a New Repository:**
   - Go to [GitHub](https://github.com) and click "New repository"
   - Name it `streamlit-workshop` 
   - Make it public and check "Add a README file"

2. **Add Requirements File:**
   - Click "Create new file" in your repo
   - Name it `requirements.txt`
   - Add these dependencies:
     ```text
     streamlit
     pandas
     scikit-learn
     matplotlib
     seaborn
     ```
   - Click "Commit new file"

3. **Launch Codespace:**
   - Click the green `<> Code` button 
   - Select "Codespaces" tab → "Create codespace on main"
   - Wait ~2 minutes for setup to complete

4. **Install Dependencies:**
   - In the terminal that opens, run:
     ```bash
     pip install -r requirements.txt
     ```

5. **Test Installation:**
   - Run: `streamlit hello`
   - Click "Open in Browser" when the popup appears
   - You should see the Streamlit demo app! ✅

**Backup Plan (Local Setup):**
*If Codespaces doesn't work, quickly set up locally:*
```bash
pip install streamlit pandas scikit-learn matplotlib seaborn
streamlit hello  # Test installation
```

> **Presenter Tip:** Have a backup Codespace ready to share if students have issues.

### 1.3: "Hello, Streamlit!" - Your First App (5 mins)

**Let's build your first app in 60 seconds!**

1. **Create the file:** In Codespaces, create `step1_hello.py`

2. **Add this code:**
   ```python
   import streamlit as st

   st.title('Hello, Streamlit! 👋')
   st.write('Welcome to my first web app!')
   ```

3. **Run it:** In terminal: `streamlit run step1_hello.py`

4. **See the magic:** Click "Open in Browser" → You've built a web app! 🎉

> **Expected Output:** A webpage with a title and welcome message

**What just happened?**
- `st.title()` creates a big heading  
- `st.write()` displays text (and much more!)
- Streamlit automatically created a web interface from your Python code



## Part 2: Streamlit Fundamentals (50 minutes)

### 2.1: Displaying Text and Data (15 mins)

**Now let's explore Streamlit's text and data display capabilities.**

Create a new file: `step2_text_data.py`

```python
import streamlit as st
import pandas as pd

st.title('Streamlit Text & Data Demo')

# Text elements - try different types
st.header('Different Text Types')
st.write("st.write() can display almost anything!")
st.text("st.text() shows plain text")
st.markdown("st.markdown() supports **bold** and *italic*")
st.code("st.code('print(hello)')")

# Data display
st.header('Data Display')
data = {
    'Product': ['Apple', 'Banana', 'Cherry'],
    'Price': [1.50, 0.50, 3.00],
    'Stock': [100, 150, 50]
}
df = pd.DataFrame(data)

st.subheader('Interactive Table (st.dataframe)')
st.dataframe(df)  # Interactive - you can sort columns!

st.subheader('Static Table (st.table)')  
st.table(df)      # Static display

# JSON/Dict display
st.subheader('Displaying JSON/Dictionary')
st.json({'status': 'success', 'items': 3, 'user': 'workshop_participant'})
```

**Run it:** `streamlit run step2_text_data.py`

> **Try This:** Click on column headers in the dataframe to sort the data!

### 2.2: Interactive Widgets (20 mins)

**This is where Streamlit becomes magical - interactive widgets that respond instantly to user input!**

Create: `step3_widgets.py`

```python
import streamlit as st

st.title('🎛️ Interactive Widgets Demo')

# Text input
st.header('User Input')
name = st.text_input('What is your name?', placeholder='Enter your name...')
if name:
    st.write(f'Hello, **{name}**! 👋')

# Number inputs  
col1, col2 = st.columns(2)
with col1:
    age = st.slider('Your age', 0, 100, 25)
with col2:
    score = st.number_input('Test score', 0, 100, 85)

st.write(f'You are {age} years old with a score of {score}')

# Selection widgets
st.header('Make Choices')
color = st.selectbox('Favorite color', ['Red', 'Blue', 'Green', 'Yellow'])
hobbies = st.multiselect('Hobbies', ['Reading', 'Gaming', 'Sports', 'Music'])

# Show results
st.header('Your Profile')
st.json({
    'name': name,
    'age': age,
    'score': score,
    'color': color,
    'hobbies': hobbies
})

# Action button
if st.button('🎉 Celebrate!'):
    st.balloons()  # Fun animation!
    st.success('Congratulations on learning Streamlit!')
```

**Run it:** `streamlit run step3_widgets.py`

> **Key Insight:** Notice how the app updates instantly as you interact with widgets - no "Submit" button needed!

### 2.3: Data Visualization (15 mins)

**Streamlit makes creating charts as easy as calling a function!**

Create: `step4_charts.py`

```python
import streamlit as st
import pandas as pd
import numpy as np

st.title('📊 Data Visualization Demo')

# Generate sample data
np.random.seed(42)  # For consistent results
data = pd.DataFrame({
    'Day': range(1, 31),
    'Sales': np.random.randint(100, 1000, 30),
    'Visitors': np.random.randint(50, 500, 30),
    'Revenue': np.random.randint(500, 5000, 30)
})

# Simple built-in charts
st.header('Built-in Charts')

col1, col2 = st.columns(2)
with col1:
    st.subheader('Line Chart')
    st.line_chart(data.set_index('Day')[['Sales', 'Visitors']])

with col2:
    st.subheader('Bar Chart') 
    st.bar_chart(data.set_index('Day')['Revenue'])

# Interactive chart selection
st.header('Interactive Chart Builder')
chart_type = st.radio('Choose chart type:', ['Line', 'Bar', 'Area'])
metric = st.selectbox('Choose metric:', ['Sales', 'Visitors', 'Revenue'])

# Display selected chart
if chart_type == 'Line':
    st.line_chart(data.set_index('Day')[metric])
elif chart_type == 'Bar':
    st.bar_chart(data.set_index('Day')[metric])
else:
    st.area_chart(data.set_index('Day')[metric])

# Raw data
with st.expander('View Raw Data'):
    st.dataframe(data)
```

**Run it:** `streamlit run step4_charts.py`

> **Cool Feature:** Try the radio buttons to switch chart types dynamically!



## Part 3: Build Your Final Project - Iris Data Explorer (40 minutes)

**Time to put it all together! We'll build a complete data dashboard using everything we've learned.**

**What we're building:** An interactive app that lets users explore the famous Iris flower dataset with filtering, visualization, and statistics.

**Learning Goals:**
- Combine widgets, data display, and charts
- Use caching for performance  
- Structure a multi-section app
- Add professional touches

### 3.1: Project Setup (5 mins)

Create our final project file: `iris_dashboard.py`

### 3.2: Building the Dashboard (30 mins)

Let's build this step by step. Start with the basic structure:

```python
import streamlit as st
import pandas as pd
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt
import seaborn as sns

# Page configuration - always first!
st.set_page_config(
    page_title="Iris Explorer",
    page_icon="🌸", 
    layout="wide"
)

# Load data with caching for performance
@st.cache_data
def load_iris_data():
    """Load and prepare the Iris dataset"""
    iris = load_iris()
    df = pd.DataFrame(iris.data, columns=iris.feature_names)
    df['species'] = iris.target_names[iris.target]
    return df, iris.DESCR

# Load the data
df, description = load_iris_data()

# === HEADER SECTION ===
st.title("Iris Flower Data Explorer")
st.markdown("Explore the classic Iris dataset interactively!")

# Show dataset info
with st.expander("About the Dataset"):
    st.write(description)

# === SIDEBAR CONTROLS ===
st.sidebar.header("Controls")

# Species filter
species_options = df['species'].unique()
selected_species = st.sidebar.multiselect(
    "Select Species to Display:",
    options=species_options,
    default=species_options,
    help="Choose which iris species to include in the analysis"
)

# Measurement filter
st.sidebar.subheader("Measurement Ranges")
sepal_length_range = st.sidebar.slider(
    "Sepal Length (cm)",
    min_value=float(df['sepal length (cm)'].min()),
    max_value=float(df['sepal length (cm)'].max()),
    value=(float(df['sepal length (cm)'].min()), float(df['sepal length (cm)'].max()))
)

# === FILTER DATA ===
filtered_df = df[
    (df['species'].isin(selected_species)) &
    (df['sepal length (cm)'] >= sepal_length_range[0]) &
    (df['sepal length (cm)'] <= sepal_length_range[1])
]

# === MAIN CONTENT ===
if filtered_df.empty:
    st.error("No data matches your current filters. Please adjust the criteria.")
else:
    # Show filtered data stats
    col1, col2, col3 = st.columns(3)
    with col1:
        st.metric("Total Samples", len(filtered_df))
    with col2:
        st.metric("Species Count", filtered_df['species'].nunique())
    with col3:
        st.metric("Avg Sepal Length", f"{filtered_df['sepal length (cm)'].mean():.1f} cm")

    # Data table
    st.subheader("Filtered Dataset")
    st.dataframe(filtered_df, use_container_width=True)

    # Visualization section
    st.subheader("Visualizations")
    
    # Chart selection
    chart_type = st.radio(
        "Choose visualization:",
        ["Scatter Plot", "Box Plot", "Histogram"],
        horizontal=True
    )
    
    # Create charts based on selection
    if chart_type == "Scatter Plot":
        fig, ax = plt.subplots(figsize=(10, 6))
        sns.scatterplot(
            data=filtered_df, 
            x='sepal length (cm)', 
            y='sepal width (cm)', 
            hue='species', 
            ax=ax,
            s=100
        )
        plt.title("Sepal Length vs Width by Species")
        st.pyplot(fig)
        
    elif chart_type == "Box Plot":
        fig, ax = plt.subplots(figsize=(10, 6))
        sns.boxplot(data=filtered_df, x='species', y='sepal length (cm)', ax=ax)
        plt.title("Sepal Length Distribution by Species")
        st.pyplot(fig)
        
    else:  # Histogram
        fig, ax = plt.subplots(figsize=(10, 6))
        for species in filtered_df['species'].unique():
            species_data = filtered_df[filtered_df['species'] == species]
            plt.hist(species_data['sepal length (cm)'], alpha=0.6, label=species, bins=15)
        plt.xlabel("Sepal Length (cm)")
        plt.ylabel("Frequency")
        plt.title("Sepal Length Distribution")
        plt.legend()
        st.pyplot(fig)

    # Summary statistics
    st.subheader("📋 Summary Statistics")
    st.dataframe(filtered_df.describe(), use_container_width=True)
```

**Run it:** `streamlit run iris_dashboard.py`

### 3.3: Testing Your Dashboard (5 mins)

Try these interactions:
- ✅ Filter different species combinations
- ✅ Adjust the sepal length slider  
- ✅ Switch between chart types
- ✅ Expand the dataset info section

**What makes this a great dashboard?**
- Clear navigation and controls
- Real-time filtering and updates
- Multiple visualization options
- Performance optimization with caching
- Professional layout with columns and metrics

## Part 4: Share Your App & Next Steps (20 minutes)

### 4.1: Deployment Demo (10 mins)

**Your app is ready to share with the world! Let's deploy it to Streamlit Cloud.**

**Prerequisites for Deployment:**
1. **GitHub Repository** with your app code
2. **Requirements file** listing dependencies  
3. **Streamlit Cloud account** (free!)

**Quick Deployment Steps:**

1. **Prepare your repository:**
   ```text
   your-repo/
   ├── iris_dashboard.py      # Your main app
   ├── requirements.txt       # Dependencies
   └── README.md             # Optional description
   ```

2. **Create requirements.txt:**
   ```text
   streamlit
   pandas
   scikit-learn
   matplotlib
   seaborn
   ```

3. **Deploy on Streamlit Cloud:**
   - Go to `streamlit.io/cloud`
   - Connect your GitHub account
   - Select repository and main file
   - Click "Deploy" → Your app goes live! 🚀

> **Live Demo:** *(Presenter should show the deployment process if time permits)*

**Result:** Your app gets a public URL like: `https://your-app.streamlit.app`

### 4.2: What You've Accomplished & Next Steps (10 mins)

**🎉 Congratulations! In 2 hours, you've learned:**

✅ **Core Streamlit Concepts**
- Text display and formatting
- Interactive widgets (sliders, selectboxes, buttons)
- Data visualization and tables
- App layout and organization

✅ **Built 4 Complete Apps**
- Hello World starter
- Text & data display demo
- Interactive widgets showcase  
- Professional data dashboard

✅ **Professional Skills**
- Code organization and structure
- Performance optimization with caching
- User interface design principles
- Deployment ready applications

## Where to Go Next

**🚀 Level Up Your Streamlit Skills:**

1. **File Uploads & Processing**
   ```python
   uploaded_file = st.file_uploader("Choose a CSV file")
   if uploaded_file:
       df = pd.read_csv(uploaded_file)
   ```

2. **Session State (Persistent Data)**
   ```python
   if 'counter' not in st.session_state:
       st.session_state.counter = 0
   ```

3. **Advanced Charts** (Plotly, Altair)
4. **Multi-page Apps** 
5. **Custom Components**

### 📚 Essential Resources

- **📖 Official Docs:** [docs.streamlit.io](https://docs.streamlit.io/)
- **🗂️ Cheat Sheet:** [docs.streamlit.io/library/cheatsheet](https://docs.streamlit.io/library/cheatsheet) 
- **🎨 App Gallery:** [streamlit.io/gallery](https://streamlit.io/gallery)
- **💬 Community:** [discuss.streamlit.io](https://discuss.streamlit.io/)
- **🎓 30 Days Challenge:** Search "30 days of Streamlit"

### 🏆 Challenge: Build Your Own App!
Try creating an app with your own data or interests. Start simple, then add features as you learn more.

**Thank you for participating! Share your creations and keep building! 🚀**
