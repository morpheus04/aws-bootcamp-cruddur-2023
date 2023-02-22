FROM python:3.10-slim-buster

# Inside Container
# Make a new folder Inside Container
WORKDIR /backend-flask


# Outside Container -> Inside Container
COPY requirements.txt requirements.txt

# Inside Container
# Install python libraries used for the app
RUN pip3 install -r requirements.txt

# Outside Container -> Inside Container
# Copy everything in the current directory
COPY . .

# Set Environment Variables (Env Vars)
ENV FLASK_ENV=development

EXPOSE ${PORT}

# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]