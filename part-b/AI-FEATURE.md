# AI Feature Specification: Smart Waitlist Prediction & Travel Assistant

## Problem It Solves

This AI feature addresses **Problem 4: PNR Status Information Is Hard To Understand** from Part A.

Many users do not know whether their Waitlist (WL), RAC, or Confirmed ticket is likely to be confirmed before the journey. They often cancel tickets unnecessarily or wait without knowing their chances.

---

# Proposed Feature – User Perspective

When a user checks their PNR status, the system displays an AI-generated prediction showing the probability of ticket confirmation.

Instead of only displaying "WL 12", the user will also see:

- Confirmation Probability: **82%**
- Expected Confirmation: **1–2 days before departure**
- Suggested Alternative Trains
- Travel Recommendation

Example:

```
Current Status

WL 12

Confirmation Probability
82%

Recommendation

High chance of confirmation.
No need to cancel now.

Alternative Trains

12622 Tamil Nadu Express
12626 Kerala Express
```

The user receives useful guidance instead of railway codes.

---

# Model or API Choice

**Model**

Google Vertex AI (Tabular Prediction Model)

Alternative:

- XGBoost Machine Learning Model

### Why this model?

- Works well with structured historical railway data.
- Fast prediction time.
- Easy deployment through REST APIs.
- High accuracy on tabular datasets.

---

# Training / Input Data

The model requires historical railway booking data.

Input Fields

- Train Number
- Source Station
- Destination Station
- Journey Date
- Class
- Quota
- Current Waitlist Position
- Historical Confirmation Rate
- Festival Season Indicator
- Weekend Indicator
- Train Occupancy
- Cancellation History

Data Sources

- IRCTC historical booking database
- Indian Railways reservation data
- PNR history
- Cancellation records

---

# AI Processing Flow

1. User enters PNR number.
2. Backend fetches booking information.
3. Booking details are sent to AI Prediction Service.
4. AI calculates confirmation probability.
5. Backend returns prediction.
6. User sees probability and recommendation.

---

# API Design

### POST /ai/waitlistPrediction

Request

```json
{
  "pnr": "1234567890"
}
```

Response

```json
{
  "probability": 82,
  "prediction": "Likely to Confirm",
  "confidence": 94,
  "recommendedAction": "Wait for confirmation",
  "alternativeTrains": [
    "12622 Tamil Nadu Express",
    "12626 Kerala Express"
  ]
}
```

---

# Frontend Changes

New Components

- AI Prediction Card
- Confirmation Probability Bar
- Recommendation Box
- Alternative Train List

New UI Elements

✔ Prediction Percentage

✔ Confidence Score

✔ Alternative Routes

✔ AI Badge

---

# Database Requirements

New Table

AI Prediction History

Fields

- Prediction ID
- User ID
- PNR Number
- Prediction Percentage
- Confidence Score
- Timestamp

---

# Confidence Threshold & Fallback

Confidence ≥ 80%

Show AI prediction.

Confidence between 50%–79%

Show prediction with warning:

"Prediction may change depending on future cancellations."

Confidence below 50%

Hide prediction and display:

"Unable to generate a reliable prediction. Please check again later."

If AI service is unavailable

Display:

"Prediction service is temporarily unavailable."

Users can still access normal PNR status.

---

# Success Metrics

- 30% reduction in customer support queries about Waitlist status.
- 40% increase in user satisfaction during PNR checking.
- Prediction accuracy above 85%.
- Reduced unnecessary ticket cancellations.
- Increased engagement with PNR Status page.

---

# Limitations & Risks

- Festival seasons may reduce prediction accuracy.
- Sudden bulk cancellations can change outcomes.
- AI predictions should not be treated as guaranteed confirmations.
- Historical data quality affects prediction performance.
- Government railway policies may change booking behavior.

---

# Future Enhancements

- Voice-based AI assistant.
- Regional language support.
- Personalized travel recommendations.
- Delay prediction integration.
- Smart notification when confirmation probability changes.

---

# Wireframe Reference

```
-------------------------------------------------
PNR STATUS

Current Status
WL 12

---------------------------------
AI Prediction

Confirmation Probability

████████░░ 82%

Likely to Confirm

Confidence: 94%

Recommendation

✔ Wait for confirmation

Alternative Trains

• Tamil Nadu Express
• Kerala Express

---------------------------------
```

This AI card appears below the existing PNR status section.