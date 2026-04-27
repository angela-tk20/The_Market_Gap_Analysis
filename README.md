#  The Sugar Trap - Market Gap Analysis


## A. Executive Summary

This analysis examined 500,000 food products from the Open Food Facts dataset across 15 snack categories to identify the Blue Ocean in the snack market , where consumer demand for healthy options is not being met by current supply. Only a small fraction of all products analysed occupy the high-protein, low-sugar quadrant (>=15g protein, <=10g sugar per 100g), confirming the market is heavily skewed toward sugary, low-protein products. The biggest market opportunity is in **[Category , auto-generated after running Sprint 4]**, where the lowest percentage of products meet the healthy zone criteria of any category analysed. An ingredients analysis of high-protein products identifies the top three protein-driving ingredients, providing clear R&D formulation guidance for the client. A Candidate's Choice Fiber Opportunity Analysis further reveals that a product combining high protein, high fiber, and low sugar would occupy a virtually untapped market position , fewer than 2% of products in the opportunity category currently meet all three criteria simultaneously.

---

## B. Project Links

| Deliverable | Link |
|---|---|
| Notebook (GitHub) | [View All Notebooks](https://github.com/angela-tk20/The_Market_Gap_Analysis) |
| Dashboard (Power BI) | [View Live Dashboard](https://app.fabric.microsoft.com/view?r=eyJrIjoiOThiZGEzODEtMGM3Ny00ZGI0LWFkZDAtMmM1M2NlYjBhOTVmIiwidCI6ImIyMGE4ZjRkLTBkNmEtNGYyZS04M2EyLTE4MWM5NjhmODg4MiIsImMiOjl9) |
| Presentation | [View Slide Deck](https://amalitech-my.sharepoint.com/:p:/p/angela_tenkorang/IQArm-hdXZAXR55XisTn1u6xAVBJeRSjY5n4rxaqQLkbB4U?e=lPNKln) |
| Video Walkthrough (Optional) | [Watch on YouTube](YOUR_YOUTUBE_LINK_HERE) |



---

## C. Technical Explanation

### Data Cleaning 
The Open Food Facts dataset was loaded as a 500,000 row sample using only 12 relevant columns, reducing memory from 3GB+ to approximately 200MB. Three cleaning steps were applied in order:
1. Dropped rows missing `product_name`, `sugars_100g`, `proteins_100g`, or `categories_tags` , these are critical for the analysis
2. Removed biologically impossible values , all nutrients are per 100g so no value can exceed 100g; anything outside [0, 100] is a data entry error
3. Deduplicated on product name + sugar + protein to remove identical repeat entries

### Category Wrangling 
The `categories_tags` column contains comma-separated tags prefixed with `en:`. We stripped these prefixes, joined all tags into a searchable string, and applied 15 priority-ordered keyword rules to assign each product one `Primary_Category`. Products not matching any rule fall into `Other Snacks` (target: under 20% of total). We expanded from 8 to 15 categories to reduce the Other Snacks bucket and better represent the diversity of snack products.

### Candidate's Choice - Triple Opportunity Analysis 
The project brief mentions High Protein AND High Fiber as consumer demand drivers, but Stories 3 and 4 only analyse sugar vs protein. We added a Triple Opportunity Index measuring what percentage of products per category meet all three criteria simultaneously: protein >= 15g, sugar <= 10g, AND fiber >= 5g per 100g.

Why this adds value:
-  fiber is stated in the business context but never measured in any other story
- Enables a stronger product claim : High Protein + High Fiber + Low Sugar commands a premium price
- Meets EU criteria for both high protein AND high fiber front-of-pack health claims simultaneously
- Reveals an even rarer market position that is harder for competitors to copy

---

## Project Structure

```
Market Gap Analysis/
├── Notebook Files/
│   ├── load_data_cleaning.ipynb
│   ├── category-wrangling.ipynb
│   ├── nutrient_matrix.ipynb
│   ├── recommendation.ipynb
│   ├── Candidate choice.ipynb
│   └── Html_exports/
├── Master-Data/
│   ├── clean_food_data.csv
│   ├── categorized_food_data.csv
│   ├── powerbi_scatter_data.csv
│   ├── powerbi_category_summary.csv
│   ├── powerbi_gap_index.csv
│   ├── powerbi_kpis.csv
│   ├── powerbi_nutriscore.csv
│   ├── powerbi_protein_sources.csv
│   ├── powerbi_triple_opportunity.csv
│   └── key_insight.txt
├── Project Documentation/
├── .gitignore
├── README.md
└── requirements.txt

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/sugar-trap-market-gap-analysis.git

# 2. Activate virtual environment
venv\Scripts\activate        # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Download dataset into Notebook Files folder
# https://static.openfoodfacts.org/data/en.openfoodfacts.org.products.csv

# 5. Run notebooks in order in Jupyter
# load_data_cleaning > category-wrangling > nutrient_matrix > recommendation > Candidate choice
```

---

## Pre-Submission Checklist

- [ ] GitHub Repo is Public (test in Incognito)
- [ ] All 5 .ipynb notebooks uploaded
- [ ] HTML export of each notebook uploaded
- [ ] Raw CSV not committed (.gitignore has *.csv)
- [ ] Power BI dashboard published (public link, no login)
- [ ] Presentation link publicly accessible
- [ ] README updated with all links
- [ ] All User Stories 1-4 complete
- [ ] Candidate's Choice explained in README


---

## Requirements

```
pandas
numpy
matplotlib
seaborn
plotly
scikit-learn
jupyter
ipykernel
```


