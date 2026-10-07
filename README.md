# 3D Music Preference Landscape

An interactive 3D visualization tool that maps musical preferences using Principal Component Analysis (PCA) and Plotly. 

The script projects both items (music tracks/videos) and raters (students/participants) into a unified 3D coordinate space:
* **Songs** appear as points: tracks with similar voting profiles across the group cluster together.
* **Listeners** appear as directional preference vectors: each vector originates from the center and points toward the tracks that person rated highest.

---

## Features

* **3D Joint Space (PCA Biplot):** Visualizes songs and listener tastes simultaneously.
* **Rater Bias Elimination:** Automatically standardizes ratings into personal z-scores ($z = \frac{x - \mu}{\sigma}$), preventing "harsh" vs. "generous" scoring baselines from distorting distances.
* **Missing Value Handling:** Missing diagonal self-ratings (when participants submit their favorite track) are automatically imputed with a score of 10.0.
* **Standalone Interactive Output:** Generates a self-contained `.html` file viewable in any modern browser with full 3D rotation, zooming, and hover tooltips.

---

## Requirements

Ensure Python 3.8+ is installed, then install the required dependencies:

```bash
pip install pandas numpy scikit-learn plotly openpyxl

```

---

## Data Preparation

The script accepts either `.csv` or `.xlsx` files. Structure your spreadsheet so that:

1. The **first column** contains the song or video titles.
2. The **subsequent columns** correspond to each participant/student.
3. The cells contain ratings (e.g., on a 1–10 scale).

### Example (`ratings.csv`):

```csv
Song,Anna,Bence,Csilla,Dániel
Bohemian Rhapsody,10,7,10,8
Blinding Lights,6,10,5,9
Smells Like Teen Spirit,9,8,10,7
Take On Me,7,6,8,10

```

> **Note on self-ratings:** If a participant left their own submitted video blank, the script will automatically treat empty/NaN values as `10.0`.

---

## Usage

1. Place `music_map.py` and your data file in the same directory.
2. Open `music_map.py` and verify the `DATA_FILE` variable points to your file:
```python
DATA_FILE = "ratings.csv"  # or "ratings.xlsx"

```


3. Run the script:
```bash
python music_map.py

```


4. A browser tab will automatically open displaying `music_landscape_3d.html`.

---

## How to Interpret the Visualization

* **Distance between songs:** Songs close to each other in 3D space received consistent, correlated ratings across the cohort, regardless of genre labels.
* **Student vector direction:** A red vector points toward the cluster of songs that participant preferred most relative to their personal baseline.
* **Opposing vectors:** If two student vectors point in roughly opposite directions ($180^\circ$), their musical tastes diverged significantly across the group's consensus dimensions.
* **Vector length:** Longer vectors indicate participants whose taste strongly aligns with the group's dominant consensus components (PC1, PC2, PC3). Shorter vectors near the origin indicate idiosyncratic, eclectic, or polarizing preferences that lie outside the main shared axes.
* **Center of the cloud:** Songs near the origin $(0, 0, 0)$ are typically universally neutral, consensus tracks with average ratings across all participants.

```

```
