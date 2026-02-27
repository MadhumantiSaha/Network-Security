# Network Security: Phishing Data Detection

### Overview
This project provides an end-to-end Machine Learning Operations (MLOps) pipeline that identifies phishing data and potential network security threats. The system covers everything from data ingestion and validation to transformation and model training. It is built using Python and exposes its functionalities via a robust **FastAPI** interface.

**🎉 Note: This project is successfully DEPLOYED!** 
The production deployment utilizes **Docker**, **AWS ECR**, and **AWS EC2**, fully automated through a **GitHub Actions CI/CD pipeline**.

### Key Features
- **Data Ingestion**: Extracts raw network data from a configured MongoDB database.
- **Data Validation & Transformation**: Validates the schema and input data, cleanses, handles anomalies, and meticulously transforms the data into ML-ready features.
- **Model Training**: Employs classification algorithms dynamically retrained via the API, saving the optimum predictive preprocessor and model.
- **FastAPI Integration**: Provides elegant RESTful routes (`/train` and `/predict`), along with a visual interactive UI.
- **Continuous Integration & Delivery (CI/CD)**: Seamless deployment processes triggered on new code pushes directly to AWS.

### Technologies Used
- **Programming Language**: Python 3.10
- **Database**: MongoDB
- **Web Framework**: FastAPI, Uvicorn, Jinja2
- **Tracking & Logging**: MLflow (AWS configuration logic supported)
- **Containerization**: Docker
- **Cloud Provider**: Amazon Web Services (AWS - ECR, EC2, IAM)
- **CI/CD**: GitHub Actions

### Architecture
1. **Core Pipeline**: `Data Ingestion` -> `Data Validation` -> `Data Transformation` -> `Model Training`. (Can be triggered locally via `main.py`).
2. **Web API**: `app.py` exposes endpoints to trigger training logic (`/train`), and prediction (`/predict`) takes a `.csv` file returning an interactive HTML classification result.

---

## 🚀 Getting Started Locally

### Prerequisites
- Python 3.10
- Conda, `uv`, or another virtual environment engine
- MongoDB instance (Atlas or local) available

### Installation
1. **Create and activate a virtual environment**:
```bash
conda create -p venv python==3.10
conda activate venv/
```
or via User-Space `uv`:
```bash
uv venv
.venv\Scripts\activate
```

2. **Install dependencies**:
```bash
pip install -r requirements.txt
# or `uv pip install -r requirements.txt`
```

3. **Set up Environment Variables**:
Create a `.env` file in the root directory and configure your MongoDB connection:
```env
MONGO_DB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/?retryWrites=true&w=majority"
```

### Running the App
Start the FastApi server utilizing the runner:
```bash
python app.py
```
*(Optionally you can run `uvicorn app:app --host 0.0.0.0 --port 8000`)*

The server will be available at: http://localhost:8000
Visit http://localhost:8000/docs for the automatically generated Swagger interactive documentation!

### API Endpoints
- **GET `/`**: Redirects to the API Swagger documentation (`/docs`).
- **GET `/train`**: Triggers the machine learning pipeline to run verifications, train the model, and save new artifacts to `final_model`.
- **POST `/predict`**: Takes an input CSV file containing raw network feature data and returns an HTML template appended with security predictions.

---

## 🌍 AWS Deployment Architecture
This application is designed specifically for a modular, cloud-native deployment. 
1. The code pushed to the `main` branch is picked up by **GitHub Actions**.
2. A deployment workflow script configures AWS credentials from Secrets and builds the **Docker Image**.
3. The image is seamlessly pushed to the **AWS Elastic Container Registry (ECR)**.
4. Lastly, the EC2 instance pulls the updated image through the Runner daemon and immediately runs the FastAPI application over port `8080` (or `8000`).

## Author
**Madhumanti**
