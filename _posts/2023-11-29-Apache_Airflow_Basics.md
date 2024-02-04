# How to Install Apache Airflow on Windows without Docker

freecodecamp.org/news/install-apache-airflow-on-windows-without-docker/


Steps:
1>. Install Linux(Ubuntu from)

First, enable the windows subsystem for Linux option in settings.

Go to Start. Search for "Turn Windows features on or off."
Check the option Windows Subsystem for Linux.
To Install

``` cmd
wsl --install
```




 airflow users create \
          --username sregmi \
          --firstname FIRST_NAME \
          --lastname LAST_NAME \
          --role Admin \
          --email sregmi@advalent.org
          
          -- Aflo@w



# Activate Env:  source airflow_env/bin/activate

# Running Webserver: airflow webserver 

# Initialize :
airflow db init 

# Check if airflow is already running:
ps aux | grep airflow
# Kill service
airflow scheduler -D



## Recommended:

Not to use sequential executor in Prod

# Executor
- Airflow executors are the mechanism that handles the running of tasks.
- 1 executor can be cofig at a time In `airflow.cfg`
- Most popular executor: Local, Celery & Kubernetes

# What is an executor?

After a DAG is defined, the following needs to happen in order for the tasks within that DAg to execute and be completed:
- The Metadata DB keeps a record of all tasks within a DAG and their corresponding status(queued, scheduled, success, running, failed etc) behind the scenes.
- The schedular reads from the Meta DB to check on the status of each task and decide what needs to get done and when
- The executor works closely with the scheduler to determine what resources will actually complete those tasks as they're queued.
- 
# Sequential Executor

-- ------------------------------------------

# Airflow WorkFlow;

The xcom_push function is used in Apache Airflow to push a value to XCom, which is a feature that allows data sharing between tasks in a workflow. The xcom_push function is called on the task instance (context[‘ti’]) to store a value with a specified key in the XCom storage.

```py
def train_iris_model_1(**context):
    # Your code for training and evaluating the Iris model with KNN algorithm (DAG 1)
    iris_data = pd.read_csv('https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data', header=None, names=['sepal_length', 'sepal_width', 'petal_length', 'petal_width', 'class'])
    iris_data['class'] = iris_data['class'].astype('category').cat.codes
    # convert into Dictionary for passing into another function using xcom_push method
    df_dict = iris_data.to_dict(orient='records')
    # Push this df_dict as an iris using xcom_push method to access in train_iris_model2 function
    context['ti'].xcom_push(key='iris', value=df_dict)
    pass
```

