# Insurance Premium Prediction API

## Project Description
This project is a FastAPI-based web service that predicts insurance premium categories based on user input data. It leverages a machine learning model to classify users into different premium categories using features such as age, BMI, lifestyle risk, city tier, income, and occupation.

## Features
- RESTful API built with FastAPI
- Input validation using Pydantic models
- Computed features including BMI, lifestyle risk, age group, and city tier
- Predicts insurance premium category using a pre-trained machine learning model
- Easy to extend and deploy

## Installation

1. Clone the repository or download the project files.
2. It is recommended to create a virtual environment:
   ```bash
   python -m venv venv
   source venv/Scripts/activate   # On Windows
   # or
   source venv/bin/activate       # On Linux/Mac
   ```
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. Start the FastAPI server using Uvicorn:
   ```bash
   uvicorn app:app --reload
   ```
2. The API will be available at `http://127.0.0.1:8000`.

3. Use the `/predict` endpoint to get insurance premium category predictions. This endpoint accepts a POST request with JSON body containing user data.

### Example Request

```bash
curl -X POST "http://127.0.0.1:8000/predict" -H "Content-Type: application/json" -d '{
  "age": 30,
  "weight": 70.5,
  "height": 1.75,
  "income_lpa": 12.5,
  "smoker": false,
  "city": "Mumbai",
  "occupation": "private_job"
}'
```

### Example Response

```json
{
  "predicted_category": "medium"
}
```

## Input Data Model Explanation

The API expects the following fields in the request body:

- `age` (int): Age of the user (0 < age < 120)
- `weight` (float): Weight of the user in kilograms (weight > 0)
- `height` (float): Height of the user in meters (0 < height < 2.5)
- `income_lpa` (float): Annual salary of the user in lakhs per annum (income_lpa > 0)
- `smoker` (bool): Whether the user is a smoker
- `city` (str): City of residence (used to determine city tier)
- `occupation` (str): Occupation of the user. One of:
  - retired
  - freelancer
  - student
  - government_job
  - business_owner
  - unemployed
  - private_job

### Computed Fields

- `bmi`: Body Mass Index calculated as weight / (height^2)
- `lifestyle_risk`: Risk level based on smoking status and BMI (high, medium, low)
- `age_group`: Categorized as young, adult, middle_aged, or senior
- `city_tier`: Tier of the city (1, 2, or 3) based on predefined city lists

## Output

The API returns a JSON response with the predicted insurance premium category as a string under the key `predicted_category`.

## Dependencies

- fastapi
- uvicorn
- pydantic
- pandas
- scikit-learn
- cloudpickle

## License

This project is licensed under the MIT License. See the LICENSE file for details.
