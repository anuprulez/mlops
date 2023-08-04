FROM huggingface/transformers-pytorch-cpu:latest
FROM python:3.8.8
COPY ./ /app



ENV PYTHON_VERSION=3.8
ENV CONDA_DIR=/home/anupkumar/anaconda3/
RUN alias python=/usr/bin/python$PYTHON_VERSION
RUN alias python3=/usr/bin/python$PYTHON_VERSION
ENV PATH=/usr/bin/python$PYTHON_VERSION:$PATH \
    PYTHON_LIB_PATH=$CONDA_DIR/lib/python$PYTHON_VERSION/site-packages

# install requirements
RUN pip install "dvc[gdrive]"
RUN pip install -r requirements_inference.txt

# initialise dvc
RUN dvc init --no-scm
# configuring remote server in dvc
RUN dvc remote add -d storage gdrive://1WSS3-CIZsZHIdRoPYkiJF5zR20cAWSSp
RUN dvc remote modify storage gdrive_use_service_account true
RUN dvc remote modify storage gdrive_service_account_json_file_path week6/galaxyworkflowmodel-e0a5e8e41574.json

# pulling the trained model
RUN dvc pull dvcfiles/trained_model.dvc


WORKDIR /app
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
