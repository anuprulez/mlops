FROM huggingface/transformers-pytorch-cpu:latest
FROM python:3.8.8

COPY ./ /app
WORKDIR /app

ARG AWS_ACCESS_KEY_ID
ARG AWS_SECRET_ACCESS_KEY


# aws credentials configuration
ENV AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID \
    AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

# install requirements
RUN pip install "dvc[s3]"   # since s3 is the remote storage
#RUN pip install -r requirements_inference.txt

# initialise dvc
RUN dvc init --no-scm -f

# configuring remote server in dvc
RUN dvc remote add -d model-store s3://models-dvc/trained_models/

RUN cat .dvc/config

# pulling the trained model
#RUN dvc pull models/model.onnx.dvc

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# running the application
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
