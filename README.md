What is Scout2?
=========

![Scout2](https://raw.githubusercontent.com/wiki/nccgroup/Scout2/images/scout2-dashboard-head.png)

Scout2 is a security tool that lets AWS administrators assess their environment's security posture. Using the AWS API, Scout2 gathers configuration data for manual inspection and highlights high-risk areas automatically. Rather than pouring through dozens of pages on the web, Scout2 supplies a clear view of the attack surface automatically.

Scout2 was designed by security consultants/auditor. It is meant to provide a point-in-time security-oriented view of the AWS account it was run in. Once the data has been gathered, all usage may be performed offline.

For engineers in order to implement periodic and/or continuous review of their AWS environment, Scout2 may be used in a CI/CD pipeline, or at the very least a scheduled job to run regularly.  

How do I setup Scout2
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

How do I use Ansible to run Scout2
=========

If you want the "Hammer Approach" you can do the following
-     [linux user@localhost ~] $  ansible-playbook -i inventory/Scout2.yml Scout2.yml --ask-vault-pass

If you would like to step into Scout2 and understand the actions a little better you can run this playbook based on tags.  There are two tags associated with this playbook.  
- "pre-flight" which sets up the host expecting to run Scout2.  
- "Scout2-run" which will run the report and drop the results into a clean Scout2-Reports directory
To run these individually please perform the follwoing
-      [linux user@localhost ~] $  ansible-playbook -i inventory/Scout2.yml Scout2.yml -t pre-flight --ask-vault-pass
-     [linux user@localhost ~] $  ansible-playbook -i inventory/Scout2.yml Scout2.yml -t scout2-run --ask-vault-pass

Adam A. Valenzuela - Brevity is the Soul of Wit.
# Ansible
