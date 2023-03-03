# Week 2 — Distributed Tracing


#### Table of Contents

+ [Required Homework](#required-homework)
  - [Instrument Honeycomb with OTEL](#instrument-honeycomb-with-otel)
  - [Run queries to explore traces within Honeycomb.io](#run-queries-to-explore-traces-within-honeycombio)
  - [Instrument AWS X-Ray into backend flask application](#instrument-aws-x-ray-into-backend-flask-application)
  - [Configure and provision X-Ray daemon within docker-compose and send data back to X-Ray API](#configure-and-provision-x-ray-daemon-within-docker-compose-and-send-data-back-to-x-ray-api)
  - [Observe X-Ray traces within the AWS Console](#observe-x-ray-traces-within-the-aws-console)
  - [Integrate Rollbar for Error Logging](#integrate-rollbar-for-error-logging)
  - [Trigger an error an observe an error with Rollbar](#trigger-an-error-an-observe-an-error-with-rollbar)
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

- Each environment has a set of API keys that needs to be used for integration (via `environment variables` with e.g. Gitpod etc. Those API keys will then be used automatically whenever Gitpod is trying to send traces to Honeycomb

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


---


### Configure and provision X-Ray daemon within docker-compose and send data back to X-Ray API


---


### Observe X-Ray traces within the AWS Console


---


### Integrate Rollbar for Error Logging


---


### Trigger an error an observe an error with Rollbar


---


### Install WatchTower and write a custom logger to send application log data to CloudWatch Log group


***




## Homework Challenges


### Instrument Honeycomb for the frontend-application to observe network latency between frontend and backend


---


### Add custom instrumentation to Honeycomb to add more attributes


---


### Run custom queries in Honeycomb
