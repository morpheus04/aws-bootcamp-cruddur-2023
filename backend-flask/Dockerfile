FROM 790852294965.dkr.ecr.us-east-1.amazonaws.com/cruddur-python:3.10-slim-buster

# Inside Container
# Make a new folder Inside Container
WORKDIR /backend-flask


# Outside Container -> Inside Container
COPY requirements.txt requirements.txt

# Inside Container
# Install python libraries used for the app
RUN pip3 install --upgrade pip -r requirements.txt

# Outside Container -> Inside Container
# Copy everything in the current directory
COPY . .

#COPY execute_flask.sh /
#RUN chmod +x /execute_flask.sh && execute_flask.sh

# Install curl to allow health check to work
RUN apt-get update -y
RUN apt-get install -y gcc
RUN apt-get install -y curl

# Set Environment Variables (Env Vars)
ENV FLASK_DEBUG=1

EXPOSE ${PORT}

# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
# CMD [ "./execute_flask.sh"]
