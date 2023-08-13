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
