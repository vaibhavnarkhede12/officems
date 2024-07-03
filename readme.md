from google.cloud import bigquery

client = bigquery.Client(project='YOUR_PROJECT_ID')

datasets = client.list_datasets()  # List all datasets in the project

for dataset in datasets:
    print(f'Dataset: {dataset.dataset_id}')
    tables = client.list_tables(dataset.dataset_id)  # List all tables in the dataset
    for table in tables:
        print(f'  Table: {table.table_id}')