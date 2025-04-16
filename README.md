

# Ministry Budget Allocation Predictor

This project provides a machine learning-based solution for predicting the **budget allocation** for various Indian government ministries based on several factors like development index, previous budgets, number of projects, priority levels, and regional impact.

It leverages **AutoGluon** for automatic model training and optimization, and provides a **Flask-based API** to make predictions via JSON inputs.

---

## Features

- Predicts budget allocation (`Allocated_Budget (Cr)`) for different ministries.
- Supports both numeric and categorical inputs.
- Accepts ministry names, priority levels, and region impact as text inputs (e.g., `"defence"`, `"high"`), which are internally label-encoded.
- Provides analysis on how different inputs affect budget predictions.
- Trained on a synthetic dataset of 10,000+ records with realistic input distributions.

---

## Dataset Description

The dataset contains the following features:

| Column Name           | Description |
|-----------------------|-------------|
| Ministry              | Name of the ministry (e.g., Health, Defence, Sports) |
| Priority_Level        | Priority assigned (High, Medium, Low) |
| Projects_Count        | Number of ongoing or proposed projects |
| Region_Impact         | Geographic focus (Urban, Rural, All) |
| Dev_Index             | Custom development index between 0–1 |
| Prev_Budget (Cr)      | Previous year’s budget in crores |
| GDP_Impact (%)        | Estimated impact of the ministry on GDP |
| Allocated_Budget (Cr) | Target column — the budget predicted by the model |

---

## Math Behind Features

- **Dev_Index**: A normalized value derived from indicators like project success rates, historical performance, and innovation levels.
- **GDP_Impact**: Estimated based on sector contribution to GDP over recent years, combined with future projections and strategic importance.
- **Priority Level**: Encoded from qualitative assessments based on urgency and national interest.

---

## Project Structure

```
ministry_budget_api/
├── app.py                   # Flask server for predictions
├── ministry_budget_dataset.csv  # Dataset used for model training
├── label_encoders.pkl      # Label encoders for categorical values
├── model/                  # Trained AutoGluon model
├── train_budget_predictor.py    # Training and testing script
└── README.md
```

---

## Getting Started

### 1. Install Requirements

```bash
pip install -r requirements.txt
```

Include packages like:

- `autogluon`
- `flask`
- `pandas`
- `scikit-learn`

### 2. Train the Model

```bash
python train_budget_predictor.py
```

This will:
- Encode categorical features
- Train and evaluate an AutoGluon model
- Save encoders and the model for API use

### 3. Start the API Server

```bash
python app.py
```

### 4. Test the API

You can send a POST request with JSON input like:

```json
{
  "Ministry": "defence",
  "Priority_Level": "high",
  "Projects_Count": 12,
  "Region_Impact": "all",
  "Dev_Index": 0.72,
  "Prev_Budget (Cr)": 48000.5,
  "GDP_Impact (%)": 3.8
}
```

---

## Output

The API will respond with the predicted allocated budget in crores:

```json
{
  "Predicted Allocated_Budget (Cr)": 50920.73
}
```

---

## Notes

- All categorical inputs are handled using label encoders.
- If you retrain the model, ensure that `label_encoders.pkl` is also updated.
- The system is designed to be scalable with real datasets in future versions.

---

Let me know if you'd like a version with GitHub-flavored markdown or if you'd like to deploy this to a cloud platform (like Heroku, AWS, etc.).
