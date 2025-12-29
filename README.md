# Premier-League-Season-Predictor

## Overview
This project uses a football match dataset (`Final_Dataset_Final.csv`) to train machine learning models that predict:

- Full-time Home Team Goals
- Full-time Away Team Goals

The model is trained on past seasons and evaluated on an unseen season (test season). In a real deployment scenario, the test season would not contain the true full-time goals — the trained model would generate those predictions.

---

## File: `Final_Dataset_Final.csv`

### What it contains
Each row represents a single match and includes:
- Match identifiers (League, Season, Date)
- Team identifiers (HomeTeam, AwayTeam)
- Match context / statistics / engineered features
- Target variables (only present in training / evaluation data):
  - Full-time home goals
  - Full-time away goals

NOTE: In the final “unseen” prediction scenario, the target columns will be removed from the test season before prediction.

---

## Goal of the Project
Given match features (teams, season, and other pre-match/engineered features), train regression models to predict:

- Home goals
- Away goals

Then use the predicted scores to:
1. Compute match outcomes (Win / Draw / Loss)
2. Aggregate results into a predicted league table for the test season

---

## Pipeline Summary

### 1. Load & Filter
- Load the CSV file
- Select a league
- Select seasons:
  - Training seasons (e.g., two past seasons)
  - Test season (held out, unseen during training)

### 2. Data Checks
- Check for null or missing values
- Confirm correct data types
- Verify target columns exist only in training data

### 3. Exploratory Data Analysis (EDA)
- Summary statistics
- Goal distributions (home vs away)
- Correlation heatmap of numeric features
- Feature vs target visualizations

### 4. Preprocessing
- One-hot encode categorical features (teams, league if needed)
- Keep numeric features unchanged
- Align train / validation / test feature columns after encoding

### 5. Split Strategy
- Time-based split to avoid data leakage:
  - Train: earlier seasons
  - Validation: later portion of training seasons
  - Test: future season

### 6. Baselines
- Mean baseline
- Median baseline
- Linear regression baseline

### 7. Models
Train two regression models:
- Model A: Home goals
- Model B: Away goals

Models used:
- Decision Tree Regressor (with hyperparameter tuning)
- Random Forest Regressor (with hyperparameter tuning)

### 8. Evaluation
Evaluate models on the test set using:
- RMSE (Root Mean Squared Error)
- MAE (Mean Absolute Error)

Optional:
- Convert predicted scores to Win / Draw / Loss
- Compute outcome prediction accuracy

### 9. Feature Importance
- Extract feature importance from tree-based models
- Optionally remove weak or uninformative features and retrain

### 10. Predicted League Table
Using predicted match scores:
- Determine match results
- Assign points (3 / 1 / 0)
- Aggregate per team:
  - Matches played
  - Wins / Draws / Losses
  - Goals for / Goals against
  - Goal difference
  - Points
- Sort by points, goal difference, and goals scored

---

## Notes / Best Practices
- Avoid data leakage by not using future-season information
- Fit encoders only on training data
- Use validation data for model selection
- Test data should be used only once for final evaluation

---

## Outputs (Recommended)
- Predicted match scores CSV
- Predicted league table CSV
- Model evaluation summary table

