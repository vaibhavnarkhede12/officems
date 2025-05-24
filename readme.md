gcloud scheduler jobs create http bq-to-pubsub-schedule \
  --schedule "*/30 * * * *" \
  --uri "https://dataflow.googleapis.com/v1b3/projects/YOUR_PROJECT_ID/locations/YOUR_REGION/templates:launch" \
  --http-method POST \
  --oauth-service-account-email your-dataflow-service-account@YOUR_PROJECT_ID.iam.gserviceaccount.com \
  --message-body '{
    "jobName": "bq-to-pubsub-$(date +%s)",
    "parameters": {}
  }'


python pipeline.py \
  --runner DataflowRunner \
  --project YOUR_PROJECT_ID \
  --region YOUR_REGION \
  --temp_location gs://YOUR_BUCKET/temp \
  --template_location gs://YOUR_BUCKET/templates/bq_to_pubsub_template


305b9-2b6e67111f-7892266488-7e69aea69c-6ffb68a0b8-43f700d2bc-cfb7e03f49-09b834e6dc-ffce5259ed-209d7f92a7-79c9ea9418-cdc3138d7a-2fe96d8516-fe31798011-69259d492f-242e188144-c728c
