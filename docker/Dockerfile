FROM apache/airflow:2.8.4

# We switch to airflow user befor installing packages
USER airflow

# We install Amazon S3 provider and pandas
RUN pip install --no-cache-dir apache-airflow-providers-amazon[s3] pandas

