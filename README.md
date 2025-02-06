# Docker Monitoring with Prometheus and Grafana

This project sets up a monitoring system for Docker containers using Prometheus and Grafana.  It leverages cAdvisor to collect container metrics and visualizes them through interactive dashboards in Grafana.

## Prerequisites

*   Docker and Docker Compose installed.  See the official Docker documentation for installation instructions: [https://docs.docker.com/](https://docs.docker.com/)

## Getting Started

1.  **Clone the repository (Optional):**  If you're starting from scratch, create the directory structure as described below.  If you have a repository, clone it:

    ```bash
    git clone <your_repository_url>
    cd monitoring  # Go into the project directory
    ```

2.  **Directory Structure:** Ensure your project has the following structure:

    ```
    monitoring/
    ├── prometheus/
    │   └── prometheus.yml
    ├── grafana/
    │   └── provisioning/
    │       └── dashboards/
    │           └── docker-dashboard.json
    ├── docker-compose.yml
    └── README.md  (This file)
    ```

3.  **Configuration:**

    *   **`prometheus/prometheus.yml`:** Configure Prometheus to scrape metrics from cAdvisor and itself.  See the example provided in the project.  Adjust `scrape_interval` and other settings as needed.
    *   **`grafana/provisioning/dashboards/docker-dashboard.json`:** This file contains the Grafana dashboard configuration.  You can create your own dashboard or use a pre-built one (see below).  **Important:** Ensure the `dataSource` name in the JSON matches your Prometheus data source name in Grafana.
    *   **`docker-compose.yml`:** This file defines the services (Prometheus, Grafana, cAdvisor) and their dependencies.  Adjust ports, volumes, and environment variables as necessary.  **Important:** Change the default Grafana admin password in this file for production environments.

4.  **Pre-built Grafana Dashboard (Optional):**

    *   You can download a pre-built Docker dashboard in JSON format. Search for "Docker" dashboards on the Grafana website or GitHub.
    *   Place the downloaded JSON file in the `grafana/provisioning/dashboards` directory.  Grafana will automatically import it on startup.

5.  **Start the Services:**

    ```bash
    docker-compose up -d
    ```

    This will download the necessary images and start the containers in detached mode.

6.  **Access the Web UIs:**

    *   **Prometheus:** `http://localhost:9090`
    *   **Grafana:** `http://localhost:3000` (default credentials: `admin/admin` - **CHANGE THIS IN PRODUCTION!**)

7.  **Grafana Data Source Configuration:**

    *   In Grafana, go to "Configuration" -> "Data sources".
    *   Add a new data source of type "Prometheus".
    *   Set the URL to `http://prometheus:9090` (within the Docker network).
    *   Save & Test.

8.  **Using the Grafana Dashboard:**

    *   If you imported a pre-built dashboard, it should be available in the Grafana dashboards list.
    *   Otherwise, you will need to create your own dashboards in Grafana using PromQL queries.

## Key Considerations

*   **Security:** Change the default Grafana password! Use strong passwords and consider other authentication methods.
*   **Alerting:** Configure alerting rules in Prometheus or Grafana to be notified of critical events.
*   **Metrics:** Explore the available cAdvisor metrics in Prometheus.
*   **Persistent Storage:** Use volumes to persist Prometheus and Grafana data for production environments.
*   **Container Names:** Use consistent container names for easier querying.
*   **PromQL:** Learn PromQL to write powerful queries and create custom dashboards.
*   **Dashboard Creation:**  Invest time in creating effective Grafana dashboards.

## Troubleshooting

*   Check the Grafana container logs: `docker-compose logs grafana`
*   Verify the data source name in your dashboard JSON.
*   Check file permissions and volume mappings.
*   Restart the Grafana container: `docker-compose restart grafana`

## Contributing

Contributions are welcome!  Please open an issue or submit a pull request.

