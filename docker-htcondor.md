# Docker jobs on HTCondor

Install HTCondor on RHEL7/CentOS7
-----------------------------------
* After installing docker, install htcondor
```bash
cd /etc/yum.repos.d
# Configure the repos
sudo wget https://research.cs.wisc.edu/htcondor/yum/repo.d/htcondor-development-rhel7.repo
sudo wget https://research.cs.wisc.edu/htcondor/yum/repo.d/htcondor-stable-rhel7.repo
# Import signing key 
sudo wget http://research.cs.wisc.edu/htcondor/yum/RPM-GPG-KEY-HTCondor
sudo rpm --import RPM-GPG-KEY-HTCondor
# Install condor
sudo yum install condor.x86_64
# Enable condor to run docker
sudo usermod -aG docker condor
# Start condor
sudo service condor start
```
* Verify that condor is up and running
```bash
$ ps -ef | grep condor
condor     22369       1  0 22:01 ?        00:00:00 /usr/sbin/condor_master -f
root       22412   22369  0 22:01 ?        00:00:00 condor_procd -A /var/run/condor/procd_pipe -L /var/log/condor/ProcLog -R 1000000 -S 60 -C 996
condor     22413   22369  0 22:01 ?        00:00:00 condor_shared_port -f
condor     22414   22369  0 22:01 ?        00:00:00 condor_collector -f
condor     22415   22369  0 22:01 ?        00:00:00 condor_negotiator -f
condor     22416   22369  0 22:01 ?        00:00:00 condor_schedd -f
condor     22417   22369  0 22:01 ?        00:00:00 condor_startd -f
condor     22459   22417  0 22:01 ?        00:00:00 kflops
cloud-u+   22461   21952  0 22:01 pts/0    00:00:00 grep --color=auto condor
$ condor_status
Name                        OpSys      Arch   State     Activity     LoadAv Mem   ActvtyTime

slot1@docker-test.novalocal LINUX      X86_64 Unclaimed Benchmarking  0.150  976  0+00:00:03
slot2@docker-test.novalocal LINUX      X86_64 Unclaimed Idle          0.000  976  0+00:00:03

                     Machines Owner Claimed Unclaimed Matched Preempting  Drain

        X86_64/LINUX        2     0       0         2       0          0      0

               Total        2     0       0         2       0          0      0
```
* Verify that condor detects that docker is installed
```bash
$ condor_status -l | grep Docker
DockerVersion = "Docker version 17.03.1-ce, build c6d412e"
HasDocker = true
StarterAbilityList = "HasDocker,HasFileTransfer,HasTDP,HasPerFileEncryption,HasVM,HasReconnect,HasMPI,HasFileTransferPluginMethods,HasJobDeferral,HasJICLocalStdin,HasJICLocalConfig"
DockerVersion = "Docker version 17.03.1-ce, build c6d412e"
HasDocker = true
StarterAbilityList = "HasDocker,HasFileTransfer,HasTDP,HasPerFileEncryption,HasVM,HasReconnect,HasMPI,HasFileTransferPluginMethods,HasJobDeferral,HasJICLocalStdin,HasJICLocalConfig"
```
