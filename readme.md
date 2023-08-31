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
