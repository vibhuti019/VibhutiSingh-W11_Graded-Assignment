# Microservices

## Author:
### Vibhuti Singh
[Portfolio](https://vibhuti019.github.io/) [GL E-PortFolio](https://eportfolio.mygreatlearning.com/vibhuti-singh2) [GitHub](https://github.com/vibhuti019) [LinkedIn](https://www.linkedin.com/in/vibhuti019/)

## Overview
This project serves a machine learning model using a Flask application. The setup includes model training, API endpoints for predictions, and containerization using Docker which was given to us as an assignment for Week 11.

## Project Structure
- `train.py`: Script for training the machine learning model.
- `app.py`: Flask application for serving the model.
- `Dockerfile`: Instructions for building the Docker image.
- `requirements.txt`: Python dependencies for the project.
- `data/breast_cancer.csv`: Dataset used for training the model.

## Training the Model
To train the model, run the `train.py` script. This script:
1. Loads and preprocesses the dataset.
2. Splits the data into training and testing sets.
3. Creates and trains an ensemble model.
4. Evaluates the model's accuracy and displays a confusion matrix.
5. Saves the trained model to `model/model_binary.dat.gz`.

## Flask API Endpoints
- `GET /info`: Returns model information and version.
- `GET /health`: Returns the health status of the service.
- `POST /predict`: Accepts JSON data and returns model predictions.

## Example cURL Commands
- **POST Predict**:
  ```sh
  curl -d '[{"radius_mean": 17.99, "texture_mean": 10.38, "perimeter_mean": 122.8, "area_mean": 1001.0, "smoothness_mean": 0.1184, "compactness_mean": 0.2776, "concavity_mean": 0.3001, "concave points_mean": 0.1471, "symmetry_mean": 0.2419, "fractal_dimension_mean": 0.07871, "radius_se": 1.095, "texture_se": 0.9053, "perimeter_se": 8.589, "area_se": 153.4, "smoothness_se": 0.006399, "compactness_se": 0.04904, "concavity_se": 0.05373, "concave points_se": 0.01587, "symmetry_se": 0.03003, "fractal_dimension_se": 0.006193, "radius_worst": 25.38, "texture_worst": 17.33, "perimeter_worst": 184.6, "area_worst": 2019.0, "smoothness_worst": 0.1622, "compactness_worst": 0.6656, "concavity_worst": 0.7119, "concave points_worst": 0.2654, "symmetry_worst": 0.4601, "fractal_dimension_worst": 0.1189}]' -H "Content-Type: application/json" -X POST http://localhost:5000/predict
  ```
- **GET Info**:
  ```sh
  curl -X GET http://localhost:5000/info
  ```
- **GET Health**:
  ```sh
  curl -X GET http://localhost:5000/health
  ```

## Docker Setup
1. **Build Docker Image**:
   ```sh
   docker build -t flask-ml-app .
   ```
2. **Run Docker Container**:
   ```sh
   docker run -p 5000:5000 flask-ml-app
   ```

## Requirements
Ensure `requirements.txt` includes:
```
Flask==2.0.1
pandas==1.3.0
scikit-learn==0.24.2
joblib==1.0.1
gunicorn==20.1.0
```

## Notes
- For production, use Gunicorn:
  ```dockerfile
  CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
  ```
- Handle configuration with environment variables.
- Use Docker volumes for data persistence if needed.
