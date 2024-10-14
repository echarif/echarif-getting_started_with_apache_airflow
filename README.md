# **Setting Up Apache Airflow on Ubuntu for Downloading Rocket Launch Data**

## **1. Create a Virtual Environment**

Start by creating a virtual environment to isolate your Python dependencies.

1. **Install `python3-venv` package** (if not already installed):
   ```bash
   sudo apt-get update
   sudo apt-get install python3-venv
   ```

2. **Create a virtual environment**:
   ```bash
   python3 -m venv airflow-env
   ```

3. **Activate the virtual environment**:
   ```bash
   source airflow-env/bin/activate
   ```

## **2. Install Apache Airflow**

1. **Upgrade `pip` and install Apache Airflow**:
   ```bash
   pip install --upgrade pip setuptools wheel
   ```

2. **Set Airflow environment variables** (adjust the home directory if needed):
   ```bash
   export AIRFLOW_HOME=~/airflow
   ```

3. **Install Apache Airflow and its dependencies**:
   Apache Airflow is installed using constraints to ensure compatibility. Run this command to install it with dependencies for the latest version:
   ```bash
   AIRFLOW_VERSION=2.7.0
   PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
   CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
   pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
   ```

4. **Initialize the Airflow database**:
   ```bash
   airflow db init
   ```

## **3. Setting up Apache Airflow Webserver and Scheduler**

1. **Start the Airflow web server** (in a separate terminal window):
   ```bash
   airflow webserver --port 8080
   ```

2. **Start the Airflow scheduler** (in a new terminal window):
   ```bash
   airflow scheduler
   ```

3. **Access the Airflow web interface** by navigating to: [http://localhost:8080](http://localhost:8080)

## **4. Create the Airflow DAG**

1. Create the `dags` folder:
   ```bash
   mkdir -p ~/airflow/dags
   ```

2. **Create the DAG file** in the `~/airflow/dags/` directory. Create the rocket_launches_dag.py file:


## **5. Trigger the DAG in Airflow**

1. In the Airflow UI, navigate to the **DAGs** page.
2. Find the `download_rocket_launches` DAG.
3. Toggle the DAG to **on** (blue slider), and click the "trigger" button (Play icon).
4. You will see the DAG tasks executed in sequence.

> **DAG Overview Screenshot Placeholder:** Insert a screenshot of the DAG overview from the Airflow UI here.

## **6. View Logs for Each Task**

1. **Download Launches Task**:
   - Click on the `download_launches` task in the Airflow UI to view its log.
   - Here you can inspect any errors or successes, such as missing dependencies.

> **Download Launches Task Log Screenshot Placeholder:** Insert a screenshot of the `download_launches` task log here.

2. **Get Pictures Task**:
   - Click on the `get_pictures` task to check the logs for the images being downloaded.
   - You can view which images were downloaded or errors, such as connection failures.

> **Get Pictures Task Log Screenshot Placeholder:** Insert a screenshot of the `get_pictures` task log here.

3. **Notify Task**:
   - Click on the `notify` task to see the notification log with the count of downloaded images.

> **Notify Task Log Screenshot Placeholder:** Insert a screenshot of the `notify` task log here.

### **7. View the DAG Graph**

1. In the Airflow UI, go to the DAGs page, select your DAG, and then click on the "Graph View" tab.
2. This will display the task execution graph showing the dependencies and the status of each task.

> **DAG Graph View Screenshot Placeholder:** Insert a screenshot of the DAG graph view from the Airflow UI here.

### **8. View the Downloaded Images**

1. The images will be downloaded to the `/tmp/images/` directory on your system. To view them, use the terminal:
   ```bash
   ls /tmp/images/
   ```

2. To verify the images, you can open them using an image viewer or move them to another directory.

> **Images Directory Screenshot Placeholder:** Insert a screenshot of the images directory listing here.

### **9. Deactivate the Virtual Environment**

When done, you can deactivate the virtual environment by running:

```bash
deactivate
```

### **10. Additional Commands**

- **To stop the Airflow web server**, use `Ctrl+C` in the terminal window where it is running.
- **To stop the scheduler**, use `Ctrl+C` in the terminal where the scheduler is running.

---

This version includes placeholders for screenshots of each task’s log, the DAG overview, and the DAG graph view in the Airflow UI.
