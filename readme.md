import json
import apache_beam as beam
from apache_beam.options.pipeline_options import PipelineOptions, StandardOptions


class FilterNullFields(beam.DoFn):
    def process(self, element):
        try:
            record = json.loads(element)
            cleaned_record = {
                k: v for k, v in record.items()
                if v not in [None, 'null', 'None']
            }
            if cleaned_record:
                yield cleaned_record
        except Exception as e:
            # Optionally handle parse errors or send to dead-letter queue
            pass


def run():
    # Update these
    project = 'your-gcp-project-id'
    subscription = 'projects/your-gcp-project-id/subscriptions/your-subscription-id'
    table_spec = 'your-gcp-project-id:your_dataset.your_table'

    options = PipelineOptions(
        streaming=True,
        project=project,
        region='us-central1',
        runner='DataflowRunner',  # Or 'DirectRunner' for local testing
        temp_location='gs://your-temp-bucket/temp',
        staging_location='gs://your-temp-bucket/staging',
        save_main_session=True
    )
    options.view_as(StandardOptions).streaming = True

    with beam.Pipeline(options=options) as p:
        (
            p
            | "Read from Pub/Sub" >> beam.io.ReadFromPubSub(subscription=subscription).with_output_types(bytes)
            | "Decode bytes" >> beam.Map(lambda x: x.decode('utf-8'))
            | "Filter null fields" >> beam.ParDo(FilterNullFields())
            | "Write to BigQuery" >> beam.io.WriteToBigQuery(
                table_spec,
                write_disposition=beam.io.BigQueryDisposition.WRITE_APPEND,
                create_disposition=beam.io.BigQueryDisposition.CREATE_NEVER,  # since table exists
                method='STREAMING_INSERTS'
            )
        )


if __name__ == '__main__':
    run()