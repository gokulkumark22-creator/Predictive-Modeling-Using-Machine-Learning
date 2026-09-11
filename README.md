# Predictive Modeling Using Machine Learning

A modern, interactive, in-browser dashboard for the full predictive modeling workflow: upload a dataset, clean it, choose an algorithm, train it, evaluate it, and generate predictions — all client-side, no backend or install required.

**[Live demo → enable GitHub Pages and this becomes a public link](#deploy-on-github-pages)**

## Features

- **Home** — project overview with an animated data visual and quick links into the workflow.
- **Upload Dataset** — drag-and-drop CSV upload (or load a built-in sample "Customer Churn" dataset), with automatic column-type detection, missing-value counts, duplicate detection, and a data preview table.
- **Data Preprocessing** — missing-value imputation or row-dropping, duplicate removal, categorical encoding, feature selection, min-max/z-score scaling, and an adjustable train/test split.
- **ML Models** — pick from Linear Regression, Logistic Regression, Decision Tree, or Random Forest, with plain-language descriptions and automatic gating based on whether your target looks like a classification or regression problem.
- **Model Training & Testing** — adjustable hyperparameters, an animated training progress bar, and a sample of predictions on the held-out test set.
- **Model Performance Dashboard** — accuracy, precision, recall, F1 (classification) or MSE, RMSE, R² (regression), plus a confusion matrix, ROC curve with AUC, feature importance chart, and an actual-vs-predicted scatter plot.
- **Prediction** — a generated input form (numeric fields + dropdowns for categorical columns) that runs new inputs through the trained model and shows the result, with class-probability bars for binary classification.

## How the machine learning works

Everything runs in the browser in plain JavaScript (`ml.js`) — there's no Python backend:

- **Linear Regression** — batch gradient descent minimizing mean squared error.
- **Logistic Regression** — gradient descent with a sigmoid output, for binary targets.
- **Decision Tree** — a CART-style tree using Gini impurity (classification) or variance reduction (regression) to choose splits.
- **Random Forest** — an ensemble of bootstrap-sampled decision trees with random feature subsets per split.

This is intentionally lightweight: it's built to demonstrate and teach the end-to-end pipeline interactively, not to replace a production Python/scikit-learn workflow. For very large files, training automatically samples down to a few thousand rows to keep the browser responsive.

## Project structure

```
├── index.html      # page structure and layout
├── styles.css       # design system and responsive layout
├── icons.js         # small inline SVG icon set
├── ml.js            # the machine learning engine (models + metrics)
├── app.js           # app state, routing, data pipeline, charts
└── README.md
```

## Run it locally

No build step or server required — just open `index.html` in a browser. If your browser blocks local file requests for the CDN scripts, serve the folder instead:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy on GitHub Pages

1. Push this folder to a GitHub repository.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch", pick your default branch and the `/ (root)` folder.
4. Save — your dashboard will be live at `https://<your-username>.github.io/<repo-name>/` within a minute or two.

## Bringing your own data

CSV files with a header row work out of the box. Numeric and categorical columns are detected automatically; pick any column as the prediction target and the dashboard will decide whether it looks like a classification or regression problem.

## Tech used

- Vanilla HTML/CSS/JavaScript (no build tooling, no framework)
- [PapaParse](https://www.papaparse.com/) for CSV parsing
- [Chart.js](https://www.chartjs.org/) for charts
- Hand-written linear algebra / ML code for the models themselves

## License

Feel free to use and adapt this project for coursework, portfolios, or demos.
