What is ScoutSuite?
=========

![ScoutSuite](https://user-images.githubusercontent.com/4206926/49877604-10457580-fe26-11e8-92d7-cd876c4f6454.png)

ScoutSuite is a security tool that lets AWS administrators assess their environment's security posture. Using the AWS API, ScoutSuite gathers configuration data for manual inspection and highlights high-risk areas automatically. Rather than pouring through dozens of pages on the web, ScoutSuite supplies a clear view of the attack surface automatically.

ScoutSuite was designed by security consultants/auditor. It is meant to provide a point-in-time security-oriented view of the AWS account it was run in. Once the data has been gathered, all usage may be performed offline.

For engineers in order to implement periodic and/or continuous review of their AWS environment, ScoutSuite may be used in a CI/CD pipeline, or at the very least a scheduled job to run regularly.  

How do I setup ScoutSuite
=========

This ansible Playbook has been setup to run on a single host, to get you ADHOC scan results in a single AWS account.  This playbook can be used with Access Keys (if running outside of AWS) or an EC2 w/ IAM ROLE (if running inside of AWS) The variables You will need to update are as follows.

- A host with Ansible 2.6 installed and verified.  
-     [linux user@localhost ~] $ "ansible --version" 
- A host with AWSCLI installed and verified 
-     [linux user@localhost ~] $ "aws --version"
- An EC2 Inatance running Centos or Ubuntu. (if running inside of AWS)
- A "ReadOnly" IAM Role to associate to the above EC2 Instance.  (if running inside of AWS)
- Valid .pem key and valid path if running from EC2. (if running inside of AWS)
- An updated inventory file so Ansible knows where to focus its attention on.
- An updated Access and Secret Keys. (if running outside of AWS)
- Verified ssh connectivity for Ansible to run.
- be sure you have an updated and ENCRYPTED vars/vars.yml

How do I use Ansible to run ScoutSuite
=========

If you want the "Hammer Approach" you can do the following
-     [linux user@localhost ~] $  ansible-playbook -i inventory/ScoutSuite.yml ScoutSuite.yml --ask-vault-pass

If you would like to step into ScoutSuite and understand the actions a little better you can run this playbook based on tags.  There are two tags associated with this playbook.  
- "pre-flight" which sets up the host expecting to run ScoutSuite.  
- "ScoutSuite-run" which will run the report and drop the results into a clean ScoutSuite-Reports directory
To run these individually please perform the follwoing
-      [linux user@localhost ~] $  ansible-playbook -i inventory/ScoutSuite.yml ScoutSuite.yml -t pre-flight --ask-vault-pass
-     [linux user@localhost ~] $  ansible-playbook -i inventory/ScoutSuite.yml ScoutSuite.yml -t ScoutSuite-run --ask-vault-pass

Adam A. Valenzuela - Brevity is the Soul of Wit.
# Ansible
