---
layout: default
title: File transfer with Globus
nav_order: 1
parent: Storage Guide
---
​Globus is a non-profit service for secure, reliable research data management (https://www.globus.org/).

Please follow [this guide](https://arcwiki.rs.gsu.edu/en/globus/transfer-data-to-iRODS) for transferring data using Globus.

### Transferring files from remote to the cluster

`remote` can be a different cluster or your local machine.

* Go to [https://www.globus.org/](https://www.globus.org/) and click on login.
* Once logged in successfully with your GSU credentials, the file manager will open.

![Globus-1]({{ site.baseurl }}/assets/images/globus1.png)

* In the "Collection" field, search for "trends", and "TRENDS_PUBLIC" should come up.

![Globus-2]({{ site.baseurl }}/assets/images/globus2.png)

* Select "TRENDS_PUBLIC".
* If you do not have one already, create your folder by selecting "New Folder" in the options menu on the right.
* Go into your folder by double-clicking on it. 
* Now you can upload files here by selecting "Upload" in the options menu on the right.

{: .hint} 
You cannot upload folders in Globus, but you can upload zipped folders and extract them on the cluster.
You can also use [scp](File_transfer_with_SCP) tool to upload folders as an alternative.

* Once the upload is complete, you can access the uploaded data on the cluster. 
Log in to the cluster and navigate to `/data/trends_public/<your folder>`.

{: .caution}
You must promptly move the uploaded data from `/data/trends_public/<your folder>` to another appropriate location on the cluster, such as `/data/users*/<your folder>`.

### Transferring files from the cluster to remote

* Log in to the cluster.
* Copy the data you want to transfer to `/data/trends_public/<your folder>`.

{: .hint}
For transferring large number of files or a folder, compress them into one or more archive files first.

{: .caution}
Be mindful of privacy rules and regulations before transferring any data out of the cluster.

* Similar to above, go to [https://www.globus.org/](https://www.globus.org/), login, and navigate your folder in the "TRENDS_PUBLIC" collection.
* Now you can download the file using "Download" in the right options menu.

{: .caution}
Once done with the transfer, remove the data from `/data/trends_public/<your folder>`.

Note that you can search for "trends" collection and use it for data transfer.