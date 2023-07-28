# Use the official lightweight Python image.
# https://hub.docker.com/_/python
FROM python:3.10

EXPOSE 8080

# Allow statements and log messages to immediately appear in the Knative logs
ENV PYTHONUNBUFFERED True

# Copy local code to the container image.
ENV APP_HOME /app
WORKDIR $APP_HOME
COPY . /app

RUN pip install -U pip
ENV CUDACXX=/usr/local/cuda/bin/nvcc
ENV CMAKE_ARGS="-DLLAMA_OPENBLAS=on"
ENV FORCE_CMAKE=1
RUN pip install -r requirements.txt
# Do these separately so the dependency conflicts are ignored.
RUN pip install -U "langchain>=0.0.240"
RUN pip install -U "chainlit>=0.6.1"
RUN pip install -U "langflow>=0.3.2"

ENTRYPOINT ["python", "-m", "chainlit", "run", "app.py", "-h", "--port", "8080"]

# docker buildx build -t chainlit-fovi-50 langflow 
# docker run -p 8080:8080 --env OPENAI_API_KEY="$OPENAI_API_KEY" chainlit-fovi-50
# gcloud builds submit --tag gcr.io/fovi-site/chainlit-fovi-50
