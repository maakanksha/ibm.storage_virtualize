Objective:
Set up mTLS and configure Policy Based Replication.

Prerequisite:
- IBM storage Virtualize ansible collection plugins must be installed

These playbook set up mTLS and configure Policy Based Replication between a primary cluster and the secondary cluster.
  - It uses storage virtualize ansible modules.
  - This playbook is designed to set up mTLS on both the site and configure Policy Based Replication between source cluster to destination cluster. This is designed in a way that it creates Data Reduction Pool , links them, creates provision policy and replication policy 
  - These playbooks also creates multiple Volumes with specified prefix along with volume group and maps all of them to the specified host 


There are total 2 files used for this use-case.
  1. PBR_variable.txt:
     This file has all the variables required for playbooks.
         - primary_cluster*     : Parameters starting with primary_cluster contain primary cluster details from where user wants to replicate data.
         - secondary_cluster*   : Parameters starting with secondary_cluster contain secondary cluster details to where volume will be replicated to
	 - volume* 		: Parameters starting volume contain details for volume such as name prefix and size for the volumes to be created.
  	 - number_of_volumes	: It is the number of volumes to be created between clusters.
	 - host_name		: It is the host name to which all the volumes should be mapped after creation. It assumes Host Ips are already assigned and                     host is already created on both clusters and are logged in.

  2. Create_PBR_config.yml:
     This playbook sets mTLS (Mutual Transport Layer Security) which includes ceritficate generation on individual cluster, export it to remote location , creates certificate store which contains the certificate bundle. This playbook creates mdiskgrp, Data reduction Pool. It links pool of both the site. It creates provision policy, replication policy. It creates voulme group and associated volumes with volume_prefix name specified in inventroy file PBR_variable.txt. It also maps all the volumes to specified host.

 Authors: Akshada Thorat  (akshada.thorat@ibm.com)
