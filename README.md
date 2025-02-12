# RiskRx: Scalable ETL Pipeline for Patient Risk Scoring

## Overview
RiskRx is an end-to-end ETL pipeline and machine learning model designed to predict patient risk levels based on structured and unstructured healthcare data. It integrates real-time and batch data sources to assess **hospital readmission risk** and **multi-disease comorbidity likelihood**. The system is built for scalability, utilizing cloud-based storage, big data frameworks, and modern ML techniques.

## Features
- **Big Data ETL** – Ingests data from APIs (FHIR, OpenFDA), SQL databases (PostgreSQL), and NoSQL stores (MongoDB, Elasticsearch).
- **Streaming Data Processing** – Handles real-time patient vitals using Apache Kafka.
- **Advanced Machine Learning** – Uses **XGBoost** and **Spark ML** for predictive modeling.
- **Cloud Integration** – Stores large-scale patient data in **Google BigQuery / AWS S3**.
- **API & Dashboard** – Exposes risk scores via **FastAPI** and visualizes insights using **Streamlit**.

## Architecture
1. **Data Ingestion**: Extracts structured and unstructured healthcare data from various sources.
2. **Data Processing**: Cleans, normalizes, and transforms data using Apache Spark and Pandas.
3. **Feature Engineering**: Extracts key features from EHRs, claims, and clinical notes using NLP models.
4. **Machine Learning Model**: Trains an XGBoost classifier to predict risk scores.
5. **Deployment**: Serves predictions via a FastAPI REST API and visualizes insights in a Streamlit dashboard.

## Technology Stack
| Component             | Technology |
|----------------------|------------|
| **Data Extraction**  | FHIR API, OpenFDA API, PostgreSQL, MongoDB |
| **Processing & ETL** | Apache Airflow, Apache Spark, Pandas, Dask |
| **Storage**         | PostgreSQL, MongoDB, Elasticsearch, Google BigQuery, AWS S3 |
| **Machine Learning** | XGBoost, Spark ML, Hugging Face Transformers (NLP) |
| **Model Serving**    | FastAPI, Docker |
| **Visualization**    | Streamlit, Tableau |

## Installation & Setup
### Prerequisites
- Python 3.8+
- Docker
- Apache Kafka (for real-time streaming)
- PostgreSQL & MongoDB

### Installation Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/jjz17/RiskRx.git
   cd RiskRx
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set up environment variables:
   ```bash
   export DATABASE_URL="postgresql://user:password@localhost:5432/riskrx"
   export MONGO_URI="mongodb://localhost:27017/"
   export FHIR_API_KEY="your_fhir_api_key"
   ```
4. Start services:
   ```bash
   docker-compose up -d  # Starts PostgreSQL, MongoDB, Kafka
   airflow scheduler & airflow webserver  # Starts Airflow
   ```
5. Run the ETL pipeline:
   ```bash
   python etl_pipeline.py
   ```
6. Start API & dashboard:
   ```bash
   uvicorn api:app --reload  # Start FastAPI server
   streamlit run dashboard.py  # Start dashboard
   ```

## API Endpoints
| Method | Endpoint          | Description |
|--------|------------------|-------------|
| GET    | `/health`        | Health check |
| POST   | `/predict`       | Predict patient risk |
| GET    | `/data/patients` | Retrieve patient records |

## Example API Request
```bash
curl -X POST "http://127.0.0.1:8000/predict" -H "Content-Type: application/json" -d '{"age": 65, "gender": "Male", "heart_rate": 95, "comorbidities": ["hypertension", "diabetes"]}'
```

## Future Improvements
- **Enhance NLP Processing** – Improve clinical text analysis using transformer models.
- **Deploy on Cloud** – Host on AWS/GCP for scalability.
- **Model Monitoring** – Implement model drift detection and continuous learning.

## Contributors
- **Jason Zhang** - [GitHub](https://github.com/jjz17) | [LinkedIn](https://linkedin.com/in/jasonjzhang)

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

