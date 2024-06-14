


gcloud compute machine-types describe n1-standard-4 --format="csv[no-heading](guestCpus,memoryMb)"


gcloud compute machine-types list --filter="guestCpus=2 AND memoryMb=2048"

gcloud alpha compute instances estimate-cost --machine-type=YOUR_MACHINE_TYPE --zone=YOUR_ZONE --billing-period=1M


SELECT pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE pid <> pg_backend_pid()
  AND datname = 'dbname';  -- replace 'dbname' with your database name






PROJECT_ID=$(curl -H "Metadata-Flavor: Google" "http://metadata.google.internal/computeMetadata/v1/project/project-id")
echo $PROJECT_ID

567654457
import jenkins.model.*
import com.cloudbees.plugins.credentials.*
import com.cloudbees.plugins.credentials.common.*

// Folder name and credentials ID
def folderName = 'MyFolder'
def credentialsId = 'my-credentials-id'

// Get the Jenkins instance
def jenkinsInstance = Jenkins.getInstance()

// Find the folder
def folder = jenkinsInstance.getItemByFullName(folderName)

// Ensure the folder exists
if (folder) {
    // Get the credentials from the folder
    def credsStore = folder.getProperties().get(com.cloudbees.hudson.plugins.folder.properties.FolderCredentialsProperty.class)
    
    if (credsStore) {
        // Find the credentials by ID
        def credentials = credsStore.getCredentials(Credentials.class).find { it.id == credentialsId }
        
        if (credentials instanceof UsernamePasswordCredentials) {
            // Extract username and password
            def username = credentials.username
            def password = credentials.password.getPlainText()
            
            // Print the username and password
            println "Username: ${username}"
            println "Password: ${password}"
        } else {
            println "Credentials not found or not of type UsernamePasswordCredentials."
        }
    } else {
        println "Folder does not have any credentials property."
    }
} else {
    println "Folder not found."
}

import com.cloudbees.plugins.credentials.CredentialsProvider
import com.cloudbees.plugins.credentials.common.StandardUsernameCredentials

// Replace 'YOUR_CREDENTIAL_ID' with the ID of your SSH Username with private key credential
def credentialId = 'YOUR_CREDENTIAL_ID'

// Retrieve the credential by its ID
def creds = CredentialsProvider.lookupCredentials(
    StandardUsernameCredentials.class,
    Jenkins.instance,
    null,
    null
).find { it.id == credentialId }

if (creds != null) {
    println "Credential ID: ${creds.id}"
    println "Username: ${creds.username}"
    // If you want to retrieve the private key, you need to cast the credential to the appropriate type
    if (creds instanceof com.cloudbees.jenkins.plugins.sshcredentials.impl.BasicSSHUserPrivateKey) {
        def privateKey = creds.getPrivateKey()
        println "Private Key: ${privateKey}"
    } else {
        println "This credential is not of type SSH Username with private key."
    }
} else {
    println "Credential with ID ${credentialId} not found."
}






import com.cloudbees.plugins.credentials.*
import com.cloudbees.plugins.credentials.domains.*

def domain = Domain.global()
def credentials = CredentialsProvider.lookupCredentials(
    StandardCredentials.class, Jenkins.getInstance(), null, domain
)

credentials.each { credential ->
    println("ID: ${credential.id}, Type: ${credential.class.simpleName}")
}



ssl_protocols TLSv1.2;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;

find /var/lib/jenkins/jobs -type f -name config.xml -exec grep -q "<definition class=\"org.jenkinsci.plugins.workflow.cps.CpsFlowDefinition\">" {} \; -print | wc -l


find /var/lib/jenkins/jobs -type f -name config.xml -exec grep -E -l "(<flowDefinition>|<org.jenkinsci.plugins.workflow.job.WorkflowJob>)" {} + | wc -l



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
