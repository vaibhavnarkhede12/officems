cat test.json | jq -c '.[]' | while read item; do
    projectname=$(echo "$item" | jq -r '.projectname')
    echo "projectname: $projectname"
    mig=$(echo "$item" | jq -r '.mig')
    echo "mig: $mig"
    region=$(echo "$item" | jq -r '.region')
    echo "region: $region"
    instanceName=$(echo "$item" | jq -r '.instanceName')
    echo "instanceName: $instanceName"
    migName=$(echo "$item" | jq -r '.migName')
    echo "migName: $migName"
done

ssl_protocols TLSv1.2;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;




Deal of the day: Urban Space 100% Cotton Curtains for Window, Room Darkening Curtains 5 feet Long with Eyelets, Set of 2 Curtains with Tieback (Passion Flower Pink, Window -5 Feet X 4 Feet) https://amzn.eu/d/doT3GlV


HUESLAND Cotton Curtains for Windows, 5 feet Long 1 Bohemian Eyelet Curtain (Window 5 x 4 ft, Green Leaf Floral) https://amzn.eu/d/8SEn47J


# /etc/google-fluentd/config.d/custom-logging.conf

<source>
  @type tail
  format none
  path /opt/logs/*.log
  pos_file /var/lib/google-fluentd/pos/custom-logging.pos
  tag custom-logs
</source>

<filter custom-logs>
  @type grep
  <regexp>
    key log
    pattern marked as failure
  </regexp>
</filter>

<match custom-logs>
  @type google_cloud
  buffer_type file
  buffer_path /var/lib/google-fluentd/buffers/custom-logs
  log_level info
  flush_interval 5s
  retry_limit 5
  num_threads 2
  time_format "%Y-%m-%dT%H:%M:%S.%NZ"
  utc
  default_resource_type global
  detect_subservice true
</match>
