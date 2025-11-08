# LISA
Linux Integrated Service Automation
As i am testing various behavior of the host system, while testing using lisa for storage related tests it requires azure environment as mentioned in the requirements, but use of lisa is for testing the storage behavior of the system storage but azure is cloud environment so when we run lisa inside the azure it tests the cloud storage but not the storage of system but in the testsuites they mentioned of azure requirement. So do you think is there any method testing storage related test cases using lisa without azure environment?
When we dive into the microsoft's current status regarding this lisa is we got an information that: LISA's xfstests are focusing on cloud storages. We're working on enabling test cases on BareMetal as well, but it needs time.

As LISA can be used in various platforms like azure, hyper v platforms here for the research purpose and to know the behaviour of lisa on the system it has been used on the debian 12 itself.
Steps to start with host machine:
Step1: Cloned LISA from GitHub using:
  # git clone https://github.com/microsoft/lisa.git
- Navigated into the LISA directory:
  # cd lisa
- Installed LISA dependencies by creating a virtual environment and using pip with pyproject.toml and additional azure dependencies.
- In older version we will be having file named requirements.txt for installing dependencies for lisa to run.
- Dependencies inside the pyproject.toml are : dependencies = [
    "assertpy ~= 1.1",
    "func-timeout ~= 4.3.5",
    "dataclasses-json ~= 0.5.2",
    "paramiko ~= 3.5.1",
    "pluggy ~= 0.13.1",
    "python-dateutil ~= 2.8.1",
    "pytest-html ~= 3.2.0",
    "PyYAML ~= 6.0.1",
    "randmac ~= 0.1",
    "retry ~= 0.9.2",
    "semver ~= 2.13.0",
    "simpleeval ~= 0.9.12",
    "spurplus ~= 2.3.5",
    "websockets ~= 13.1",
    "charset_normalizer ~= 2.1.1",
    "requests ~= 2.32.4",
]
- But in newer version we have all dependencies in a pyproject.toml, then execute below commands to get dependencies of lisa and azure dependencies in requirements.txt and another.txt respectively.
# pip install --break-system-packages -r requirements.txt
You get installed with: assertpy ~= 1.1
func-timeout ~= 4.3.5
dataclasses-json ~= 0.5.2
paramiko ~= 3.5.1
pluggy ~= 0.13.1
python-dateutil ~= 2.8.1
pytest-html ~= 3.2.0
PyYAML ~= 6.0.1
randmac ~= 0.1
retry ~= 0.9.2
semver ~= 2.13.0
simpleeval ~= 0.9.12
spurplus ~= 2.3.5
websockets ~= 10.3
charset_normalizer ~= 2.1.1
requests ~= 2.32.4

Optional but recommended for Azure/local VM operations
msrestazure ~= 0.6.4
azure-identity ~= 1.17.0b1
azure-mgmt-compute ~= 30.5.0
azure-mgmt-network ~= 19.3.0
azure-mgmt-resource ~= 21.0.0
azure-storage-blob ~= 12.23.0
azure-storage-file-share ~= 12.18.0
azure-keyvault-secrets ~= 4.7.0
azure-keyvault-certificates ~= 4.7.0
pycdlib ~= 1.12.0
cachetools ~= 5.2.0
Pillow <= 11.1.0
Add the below dependencies in the newly created text file named another.txt
# pip install –break-system-packages -r another.txt
You get installed with:
azure-identity~=1.17.0b1
azure-mgmt-compute~=30.5.0
azure-mgmt-keyvault~=10.2.3
azure-mgmt-marketplaceordering~=1.1.0
azure-mgmt-msi~=7.0.0
azure-mgmt-network~=19.3.0
azure-mgmt-privatedns~=1.0.0
azure-mgmt-resource~=21.0.0
azure-mgmt-serialconsole~=1.0.0
azure-mgmt-storage~=21.2.1
azure-storage-blob~=12.23.0
azure-storage-file-share~=12.18.0
azure-keyvault-secrets~=4.7.0
azure-keyvault-certificates~=4.7.0
msrestazure~=0.6.4
cachetools~=5.2.0
Pillow<=11.1.0
- Created a `requirements.txt` and ‘anothermanually from pip errors encountered (e.g., dataclasses_json, pluggy, msrestazure, libvirt).
We want ssh keys for lisa to access our machine so ley's setup ssh key values
SSH key generated with:
# ssh-keygen -t rsa -b 4096 -f ~/.ssh/mariner_key
- Confirmed SSH key files: mariner_key (private), mariner_key.pub (public)
- Verified SSH access to VM using the key.
# python3 -m lisa -r microsoft/runbook/ready.yml -v "public_address:127.0.0.1" -v "user_name:rujwal" -v "admin_private_key_file:/home/rujwal/.ssh/mariner_key"
After running this, lisa access the machine and for default verify_cpu_count test case will be tested. 
