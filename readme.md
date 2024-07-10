from google.cloud import bigquery

client = bigquery.Client(project='YOUR_PROJECT_ID')

datasets = client.list_datasets()  # List all datasets in the project

for dataset in datasets:
    print(f'Dataset: {dataset.dataset_id}')
    tables = client.list_tables(dataset.dataset_id)  # List all tables in the dataset
    for table in tables:
        print(f'  Table: {table.table_id}')



        Certainly! Here’s a brief writeup for referring a DevOps engineer with expertise in automation, Python, Terraform, GCP, and Linux:

---

**Referral for DevOps Engineer**

I am pleased to recommend [Candidate's Name] for the position of DevOps Engineer. With a robust background in automation and extensive hands-on experience in Python, Terraform, Google Cloud Platform (GCP), and Linux, [Candidate's Name] exemplifies the qualities of a top-tier professional in the DevOps field.

**Key Skills and Achievements:**

1. **Automation Expertise:** [Candidate's Name] has a proven track record of automating complex workflows and processes, significantly enhancing operational efficiency and reducing manual intervention. They have developed and maintained numerous automation scripts and tools using Python, ensuring seamless integration and continuous delivery pipelines.

2. **Proficiency in Python:** Their in-depth knowledge of Python has enabled them to create robust automation scripts, implement infrastructure as code (IaC) solutions, and develop custom monitoring tools. Their coding skills are complemented by best practices in version control and collaborative development.

3. **Terraform Mastery:** [Candidate's Name] has extensive experience with Terraform, demonstrating the ability to design, implement, and manage scalable infrastructure on various cloud platforms. Their expertise includes writing modular and reusable Terraform configurations, managing state files, and integrating Terraform with CI/CD pipelines.

4. **Google Cloud Platform (GCP):** With hands-on experience in GCP, [Candidate's Name] has successfully architected and managed cloud environments, leveraging services such as Compute Engine, Kubernetes Engine, Cloud Storage, and BigQuery. They have a strong understanding of GCP’s networking, security, and cost optimization strategies.

5. **Linux Proficiency:** [Candidate's Name] possesses deep knowledge of Linux operating systems, enabling them to manage and troubleshoot server environments effectively. They are adept at shell scripting, system administration, and ensuring system security and performance.

**Professional Attributes:**

- **Problem-Solving:** [Candidate's Name] has demonstrated exceptional problem-solving skills, tackling complex challenges with innovative solutions and a keen eye for detail.
- **Collaboration:** They are a team player who thrives in collaborative environments, effectively communicating with cross-functional teams to achieve project goals.
- **Continuous Learning:** [Candidate's Name] is committed to staying current with industry trends and technologies, continually expanding their skill set and applying new knowledge to their work.

**Conclusion:**

[Candidate's Name] is an outstanding DevOps engineer whose expertise in automation, Python, Terraform, GCP, and Linux makes them an invaluable asset to any organization. I am confident that their technical skills, combined with their professional attributes, will contribute significantly to the success of your team.

---

If you
