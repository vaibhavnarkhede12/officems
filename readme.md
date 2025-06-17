set GCP_ENV=dev
set REGION=europe-west2
set NUM_WORKERS=1
set PROJECT=hsbc-11393281-ihubecud1-%GCP_ENV%
set TEMPLATE_BUCKET=gs://%PROJECT%-esp-template
set BUCKET=gs://%PROJECT%-esp-tmp
set KMS_PROJECT=hsbc-63207744-kms-%GCP_ENV%
set JOB_NAME=bq_to_gcs_test

REM Debugging environment variables
echo GCP_ENV=%GCP_ENV%
echo REGION=%REGION%
echo NUM_WORKERS=%NUM_WORKERS%
echo PROJECT=%PROJECT%
echo TEMPLATE_BUCKET=%TEMPLATE_BUCKET%
echo BUCKET=%BUCKET%
echo KMS_PROJECT=%KMS_PROJECT%
echo JOB_NAME=%JOB_NAME%

REM Running the Python script
python bq_to_gcs.py ^
  --job_name %JOB_NAME% ^
  --region %REGION% ^
  --project %PROJECT% ^
  --runner DataflowRunner ^
  --subnetwork https://www.googleapis.com/compute/v1/projects/hsbc-63207744/vpcHost-eu-%GCP_ENV%/regions/%REGION%/subnetworks/cinternal-vpc1-%REGION% ^
  --service_account_email=event-refinery@%PROJECT%.iam.gserviceaccount.com ^
  --temp_location %BUCKET%/tmp/ ^
  --template_location %TEMPLATE_BUCKET%/templates/%JOB_NAME%.json ^
  --no_use_public_ips ^
  --setup_file=./setup.py ^
  --autoscaling_algorithm THROUGHPUT_BASED ^
  --max_num_workers=2 ^
  --num_workers=%NUM_WORKERS% ^
  --machine_type=n1-standard-2 ^
  --experiments=use_network_tags;tt-11393281-ihubecud1-gcp-a-e-dataflow;tt-11393281-ihubecud1-dataflow-a-e-aws;tt-11393281-ihubecud1-dataflow-a-i-dataflow ^
  --experiments=use_runner_v2 ^
  --experiments=enable_kms_on_streaming_engine



set GCP_ENV=dev
set REGION=europe-west2
set NUM_WORKERS=1
set MAX_WORKERS=3
set PROJECT=hsbc-11393281-ihubecud1-%GCP_ENV%
set TEMPLATE_BUCKET=gs://%PROJECT%-temp-template
set BUCKET=gs://%PROJECT%-esp-tmp
set KMS_PROJECT=hsbc-63207744-kms-%GCP_ENV%
set JOB_NAME=bq_to_gcs_bat

gcloud --project=%PROJECT% dataflow jobs run %JOB_NAME%-%TX% ^
--gcs-location=gs://%TEMPLATE_BUCKET%/templates/%JOB_NAME%.json ^
--region=%REGION% ^
--service-account=event_refinery@%PROJECT%.iam.gserviceaccount.com ^
--staging-location=%BUCKET%/ ^
--subnetwork=https://www.googleapis.com/compute/v1/projects/%KMS_PROJECT%/regions/%REGION%/subnetworks/cinternal-vpc1-%REGION% ^
--num-workers=%NUM_WORKERS%