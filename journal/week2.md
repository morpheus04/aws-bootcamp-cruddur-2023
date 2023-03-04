# Week 2 — Distributed Tracing


#### Table of Contents

+ [Required Homework](#required-homework)
  - [Instrument Honeycomb with OTEL](#instrument-honeycomb-with-otel)
  - [Run queries to explore traces within Honeycomb.io](#run-queries-to-explore-traces-within-honeycombio)
  - [Instrument AWS X-Ray into backend flask application](#instrument-aws-x-ray-into-backend-flask-application)
  - [Configure and provision X-Ray daemon within docker-compose and send data back to X-Ray API](#configure-and-provision-x-ray-daemon-within-docker-compose-and-send-data-back-to-x-ray-api)
  - [Observe X-Ray traces within the AWS Console](#observe-x-ray-traces-within-the-aws-console)
  - [Integrate Rollbar for Error Logging](#integrate-rollbar-for-error-logging)
  - [Trigger an error and observe an error with Rollbar](#trigger-an-error-and-observe-an-error-with-rollbar)
  - [Install WatchTower and write a custom logger to send application log data to CloudWatch Log group](#install-watchtower-and-write-a-custom-logger-to-send-application-log-data-to-cloudwatch-log-group)

      
* [Homework Challenges](#homework-challenges)
  - [Instrument Honeycomb for the frontend-application to observe network latency between frontend and backend](#instrument-honeycomb-for-the-frontend-application-to-observe-network-latency-between-frontend-and-backend)
  - [Add custom instrumentation to Honeycomb to add more attributes](#add-custom-instrumentation-to-honeycomb-to-add-more-attributes)
  - [Run custom queries in Honeycomb](#run-custom-queries-in-honeycomb)



## Required Homework


### Instrument Honeycomb with OTEL

- Created HoneyComb Account

HoneyComb Account create and linked to GitHub.

- Created new environment

![image](https://user-images.githubusercontent.com/37842433/222771769-37c89cd7-e7ef-4cf2-8a92-4170af375287.png)

- Each environment has a set of API keys that needs to be used for integration (via `environment variables`) with e.g. Gitpod etc. Those API keys will then be used automatically whenever Gitpod is trying to send traces to Honeycomb

![image](https://user-images.githubusercontent.com/37842433/222772564-77003f1f-bfef-40fa-a959-19d6f0028f6a.png)

- Set Gitpod `environment variables` using the HoneyComb API keys. 

```sh
export HONEYCOMB_API_KEY="REDACTED"
export HONEYCOMB_SERVICE_NAME="Cruddur"

gp env HONEYCOMB_API_KEY="REDACTED"
gp env HONEYCOMB_SERVICE_NAME="Cruddur"
```

- Modify docker-compose file to add `env vars`

[Commit link to 35fc97e](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/35fc97e5440b4381b011890025c0cea30b42a07d?diff=split#diff-e45e45baeda1c1e73482975a664062aa56f20c03dd9d64a827aba57775bed0d3)


- Modify docker-compose file to add OpenTelemetry variables for the backend-flask service

:warning: **Warning:** I had to set the `HONEYCOMB_SERVICE_NAME` variable globally for this task, however it is not recommended for production as this should be set per service!

[Commit link to adding HONEYCOMB_SERVICE_NAME](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/35fc97e5440b4381b011890025c0cea30b42a07d?diff=split#diff-e45e45baeda1c1e73482975a664062aa56f20c03dd9d64a827aba57775bed0d3)

- Install the Python modules for OpenTelemetry

[This was done by adding the dependencies to the `requirements.txt`](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/35fc97e5440b4381b011890025c0cea30b42a07d?diff=split#diff-55d5801c5f315ed423b03e986f4ecf1d3915c097ac8c66c733f0e4cbc17cfee3)

```sh
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```

Then install these OpenTelemetry dependencies:
`pip install -r requirements.txt`

- Libraries Import Add to app.py

`opentelemetry` modules need to import the required libraries to carry out instructions. This is seen in the [commit link](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/35fc97e5440b4381b011890025c0cea30b42a07d?diff=split#diff-0014cc1f7ffd53e63ff797f0f2925a994fbd6797480d9ca5bbc5dc65f1b56438)

- Initialize automatic instrumentation with Flask

These instruction should be in the main app function `app = Flask(__name__)` as seen in the [commit link](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/35fc97e5440b4381b011890025c0cea30b42a07d?diff=split#diff-0014cc1f7ffd53e63ff797f0f2925a994fbd6797480d9ca5bbc5dc65f1b56438)

- Run Backend app via docker-compose file

Ran the `docker-compose.yml` file just for the backend app

```sh
# HoneyComb ----------
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```

  - Dataset "Cruddur" was created
  
  ![image](https://user-images.githubusercontent.com/37842433/222801270-3962d958-5b1f-41fe-ab35-0f48e00f83e0.png)
  

- Added a Span to create traces

Modified `home_activities.py` by adding the code below

``` sh
from opentelemetry import trace
tracer = trace.get_tracer("home.activities")
```

- Create Mock Data Span
  - Modified the class `HomeActivities`
  - inside `def run()` function of `home_activities.py` by adding the code below

```sh
with tracer.start_as_current_span("home-activities-mock-data"): now = datetime.now(timezone.utc).astimezone()
```

- Span Result

![image](https://user-images.githubusercontent.com/37842433/222801847-b6fbd8cc-b9de-41fe-aadd-7e0e78fdb9e8.png)

 
---


### Run queries to explore traces within Honeycomb.io

Ran query to get `AVG, COUNT of http_code=200`

![image](https://user-images.githubusercontent.com/37842433/222807146-fd93a979-0e79-43c8-a10a-3d526e12dc1c.png)

Traces

![image](https://user-images.githubusercontent.com/37842433/222808345-3ca4b2c7-683d-45b9-9cd2-23efd4c4a48f.png)



---


### Instrument AWS X-Ray into backend flask application

- Install the Python modules for AWS X-RAY

This was done by adding the dependencies to the `requirements.txt`

```
aws-xray-sdk
```

---


### Configure and provision X-Ray daemon within docker-compose and send data back to X-Ray API

- Added X-Ray Daemon to `docker-compose.yml` file

:warning: **Warning:** I had to set the `AWS_REGION` variable globally for this task in Gitpod

```sh
xray-daemon:
    image: "amazon/aws-xray-daemon"
    environment:
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
      AWS_REGION: "${AWS_REGION}"
    command:
      - "xray -o -b xray-daemon:2000"
    ports:
      - 2000:2000/udp
```

- Added required environment variables to `docker-compose.yml` file

```sh
services:
  backend-flask:
    environment:
    ...
      AWS_XRAY_URL: "*4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}*"
      AWS_XRAY_DAEMON_ADDRESS: "xray-daemon:2000"
 ```

---


### Observe X-Ray traces within the AWS Console

- Backend app trace

![image](https://user-images.githubusercontent.com/37842433/222815134-82059ab0-d936-4d8b-adc5-bc71bc7dbb94.png)


- Further queries

![image](https://user-images.githubusercontent.com/37842433/222815912-d6905775-7086-4544-aec8-bf71e723c537.png)


---


### Integrate Rollbar for Error Logging

- Install the Python modules for Rollbar

This was done by adding the dependencies to the `requirements.txt`

```
rollbar
```

- Import Libraries into `app.py`

```sh
# Rollbar --------
import rollbar
import rollbar.contrib.flask
from flask import got_request_exception
```

- Initialise tracing of Rollbar

```sh
# Rollbar ---------
# Initialize tracing and an exporter that can send data to Rollerbar
rollbar_access_token = os.getenv('ROLLBAR_ACCESS_TOKEN')
@app.before_first_request
def init_rollbar():
    """init rollbar module"""
    rollbar.init(
        # access token
        rollbar_access_token,
        # environment name
        'production',
        # server root directory, makes tracebacks prettier
        root=os.path.dirname(os.path.realpath(__file__)),
        # flask already sets up logging
        allow_logging_basic_config=False)

    # send exceptions from `app` to rollbar, using flask's signal system.
    got_request_exception.connect(rollbar.contrib.flask.report_exception, app)
```

- Create Endpoint

```sh
@app.route('/rollbar/test')
def rollbar_test():
    rollbar.report_message('Hello World!', 'warning')
    return "Hello World!"
```

- Rollbar Item

![image](https://user-images.githubusercontent.com/37842433/222822871-47db714d-7288-49d2-b0dd-b3d67dfe4008.png)


- Payload Test

![image](https://user-images.githubusercontent.com/37842433/222823314-a317756c-b832-472d-85d7-2700c7eb59f5.png)


- Payload result

```sh
{
  "body": {
    "message": {
      "body": "Hello World!"
    }
  },
  "uuid": "00f5983f-76d8-4512-9793-43a1bcdec1f7",
  "language": "python 3.10.10",
  "level": "warning",
  "timestamp": 1677875175,
  "server": {
    "root": "/backend-flask",
    "host": "761bc03cbff9",
    "pid": 27,
    "argv": [
      "/usr/local/lib/python3.10/site-packages/flask/__main__.py",
      "run",
      "--host=0.0.0.0",
      "--port=4567"
    ]
  },
  "environment": "production",
  "framework": "flask",
  "notifier": {
    "version": "0.16.3",
    "name": "pyrollbar"
  },
  "metadata": {
    "customer_timestamp": 1677875174
  }
}
```

---


### Trigger an error and observe an error with Rollbar

- To trigger an error;
  - modified the `home_activities.py` file
  - modified the `HomeActivities` class
  ```sh
  # Create Span
  from opentelemetry import trace
  tracer = trace.get_tracer("home.activities")

  class HomeActivities:
    def run():
      with tracer.start_as_current_span("home-activities-mock-data"): now = datetime.now(timezone.utc).astimezone()
  ```
  
  - Error was then generated in Rollbar

![image](https://user-images.githubusercontent.com/37842433/222825350-a60cadb8-287e-43e8-9d5d-8829624818cc.png)


---


### Install WatchTower and write a custom logger to send application log data to CloudWatch Log group

- Install the Python modules for WatchTower

This was done by adding the dependencies to the `requirements.txt`

```
watchtower
```


- Import Libraries into `app.py`

```sh
# WatchTower & Cloudwatch Logs ---------
import watchtower
import logging
from time import strftime
```


- Logger Configuration

```sh
# Configuring Logger to Use CloudWatch
LOGGER = logging.getLogger(__name__)
LOGGER.setLevel(logging.DEBUG)
console_handler = logging.StreamHandler()
cw_handler = watchtower.CloudWatchLogHandler(log_group='cruddur')
LOGGER.addHandler(console_handler)
LOGGER.addHandler(cw_handler)
LOGGER.info("some message")
```


- Logger Configuration for Cloudwatch Integration

```sh
# Configuring Logger to Use CloudWatch
LOGGER = logging.getLogger(__name__)
LOGGER.setLevel(logging.DEBUG)
console_handler = logging.StreamHandler()
cw_handler = watchtower.CloudWatchLogHandler(log_group='cruddur')
LOGGER.addHandler(console_handler)
LOGGER.addHandler(cw_handler)
LOGGER.info("Home testing Activities")
```


- Set the env var in your backend-flask for `docker-compose.yml` file

```sh
      AWS_DEFAULT_REGION: "${AWS_DEFAULT_REGION}"
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
```


- Cloudwatch Result & Log Group


![image](https://user-images.githubusercontent.com/37842433/222923907-438df324-464b-48cb-be80-483aea893c18.png)


***




## Homework Challenges


### Instrument Honeycomb for the frontend-application to observe network latency between frontend and backend

- Install Open Telemetry packages

```sh
npm install --save \
    @opentelemetry/api \
    @opentelemetry/sdk-trace-web \
    @opentelemetry/exporter-trace-otlp-http \
    @opentelemetry/context-zone
```

---


### Add custom instrumentation to Honeycomb to add more attributes

- Custom span with a User ID

[Commit link](https://github.com/morpheus04/aws-bootcamp-cruddur-2023/commit/f8c9a61a19386086f3328e2bd2c503ecd12c52a6?diff=split#diff-e7fc4f0f2b4e4510d81bbc953fe4e4198587359967fc005d49cb23f39e7f3130)

![image](https://user-images.githubusercontent.com/37842433/222926608-be6c5b3d-79f7-4071-9c49-7075856b4a4f.png)


---


### Run custom queries in Honeycomb

- Custom query based on `app.user_id`

![image](https://user-images.githubusercontent.com/37842433/222926905-7adc392a-93f0-41ad-8b48-e0bab82ad155.png)


