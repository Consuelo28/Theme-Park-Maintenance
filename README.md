# Theme-Park-Maintenance
Predictive Maintenance Platform for Theme Park Animatronics

Overview:
This project was developed for the IoT & Cloud Technologies course at SRH University Berlin. The platform demonstrates how IoT and cloud technologies can be used to transform theme park animatronic maintenance from a reactive process into a proactive predictive maintenance system.
The system simulates real-time sensor data from animatronics, securely transmits the data through an MQTT-based pipeline, stores it in Google Cloud BigQuery, and visualizes it through an interactive Streamlit dashboard with real-time monitoring and anomaly detection capabilities.
__________________________________________________________________
Problem Statement:
Theme park animatronics operate under intensive mechanical and thermal conditions, often running for extended duty cycles throughout the day. Traditional maintenance strategies rely heavily on fixed schedules or reactive repairs after failures occur, which can lead to:
- Unexpected ride downtime
- High repair costs
- Reduced guest experience
- Increased mechanical wear
- Limited visibility into asset health
This project introduces a cloud-connected IoT ecosystem capable of continuously monitoring animatronic performance and detecting abnormal behaviour before critical failures occur.
__________________________________________________________________
System Architecture: 
- The platform follows an end-to-end Edge-to-Cloud IoT architecture
  
Animatronic Sensors (Temperature, Vibration, Power Draw) → Python Sensor Simulator (robot_sim.py) → MQTT Broker (EMQX / Eclipse Mosquitto) → Dockerized IoT Gateway → Google Cloud BigQuery → Streamlit Dashboard (Real-Time Monitoring & Alerts)
__________________________________________________________________
Features:
- Real-time animatronic telemetry simulation
- Monitoring of:
    - Temperature
    - Vibration
    - Power draw
- MQTT-based communication
- Dockerized IoT gateway
- Secure cloud ingestion pipeline
- Real-time Streamlit dashboard
- Interactive charts and tables
- Multi-animatronic monitoring
- Auto-refreshing dashboard every 5 seconds
- Real-time anomaly detection and alerts
- Cloud-based data persistence using BigQuery
__________________________________________________________________
Technologies used: 
| Category          | Technologies                         |
| ----------------- | ------------------------------------ |
| Programming       | Python                               |
| IoT Communication | MQTT                                 |
| MQTT Broker       | EMQX / Eclipse Mosquitto             |
| Containerization  | Docker                               |
| Cloud Platform    | Google Cloud Platform (GCP)          |
| Data Warehouse    | Google BigQuery                      |
| Visualization     | Streamlit                            |
| Security          | TLS Encryption, IAM Service Accounts |
__________________________________________________________________
IoT & Cloud Implementation: 
Edge / IoT Layer
The edge layer simulates three animatronics with sensor readings generated for:
- Temperature
- Vibration
- Electrical power draw
The Python simulator publishes telemetry data through MQTT topics to the broker running inside a Docker container.
To optimize bandwidth efficiency and cloud ingestion costs, the system uses a 5-second sampling interval, providing deterministic dashboard updates while reducing unnecessary network overhead.
__________________________________________________________________
Cloud Layer:
The cloud layer uses Google BigQuery as a scalable serverless data warehouse for storing telemetry data in real time.
A Python-based IoT gateway subscribes to MQTT topics, processes incoming telemetry, and inserts records directly into BigQuery using a Google Cloud Service Account.
The system follows an event-driven architecture, where MQTT messages trigger callback functions that process and upload sensor readings asynchronously.
__________________________________________________________________
Security:
The platform implements secure telemetry transmission through:
- TLS encryption for MQTT and cloud communication
- Google Cloud IAM Service Accounts with restricted permissions
- Secure transmission of telemetry data before cloud storage
This ensures that sensor data remains protected while in transit between the edge layer and cloud infrastructure.
__________________________________________________________________
Dashboard Functionality
The Streamlit dashboard provides:
- Real-Time Monitoring
    - Live telemetry updates every 5 seconds
    - Interactive charts for sensor metrics
    - Real-time data tables
- Multi-Animatronic Navigation
    - Sidebar containing all monitored animatronics
    - Ability to switch between assets dynamically
- Anomaly Detection
The system generates alerts when abnormal conditions are detected, including:
    - Overheating
    - Excessive vibration
    - Abnormal power consumption
Each alert includes the reason for the anomaly to support maintenance decision-making.
__________________________________________________________________
Performance Optimization:
During development, the dashboard initially experienced full-page refresh flickering caused by Streamlit’s top-to-bottom execution model.
This was resolved using:
- Fragment-based architecture (@st.fragment)
- Partial rerendering of charts and data
- Preserved sidebar state management
This significantly improved dashboard responsiveness and user experience.
__________________________________________________________________
Installation: 
1. Clone the Repository
    - git clone https://github.com/Consuelo28/Theme-Park-Maintenance.git
    - cd Theme-Park-Maintenance
2. Install dependencies:
  - pip install -r requirements.txt
3. Configure Google Cloud Credentials:
  - Add your Google Cloud Service Account Key.
  - Ensure the service account has permission to write to your BigQuery table.
4. Run Docker Services:
  - docker compose up
5. Start the Streamlit Dashboard
  - streamlit run dashboard.py
__________________________________________________________________
Future Improvements:
Planned future enhancements include:
- Machine learning-based anomaly prediction
- Edge AI deployment inside Docker containers
- Automated Slack/email maintenance notifications
- Secure device identification framework
- Kubernetes-based scaling for large animatronic fleets
- Map-based monitoring of global theme park assets
__________________________________________________________________
Learning Outcomes:
This project demonstrates practical implementation of:
- IoT device communication
- MQTT telemetry pipelines
- Event-driven systems
- Edge-to-cloud architectures
- Real-time data visualization
- Cloud-native storage solutions
- Containerized infrastructure
- Secure cloud communication
__________________________________________________________________
Course Information:
Developed for the IoT & Cloud Technologies course at SRH University Berlin.
__________________________________________________________________
Authors:
Consuelo Cornejo Antilef & Clara Rowe
__________________________________________________________________
License:
This project was developed for academic purposes.
