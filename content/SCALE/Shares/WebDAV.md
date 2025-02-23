---
title: "WebDAV Shares"
weight: 40
---

{{< toc >}}

WebDAV stands for Web-based Distributed Authoring and Versioning, which is an extension to HTTP. In TrueNAS, WebDAV shares can be created so that authenticated users can browse the contents of a specified pool, dataset, or directory from a web browser.

{{< include file="static/includes/General/SharingPrereqs.md.part" markdown="true" >}}

## Share Configuration 

Go to **Shares > WebDAV** and click *Add*.

![SharingWebdavAdd](/images/SCALE/SharingWebdavADD.png "Creating a WebDAV Share")

Enter a share *Name* and use the file browser to select the dataset to be shared. An optional *Description* helps to identify the share. To prevent user accounts from modifying the shared data, set *Read Only*.

By default, *Change User & Group Ownership* is set.
This changes the existing ownership of *ALL* files in the share to the *webdav* user and group accounts.
This behavior simplifies WebDAV share permissions, but is unexpected, so the web interface shows a warning:

![Webdav Add Warning](/images/SCALE/SharingWebdavAddWarning.png "Services Webdav Add Warning")

Setting the *Confirm* checkbox and clicking *OK* will create the share.

{{< hint info >}}
This warning does not show when *Change User & Group Ownsership* is unset.
In that situation, shared file ownership must be manually set to the *webdav* or *www* user and group accounts.
{{< /hint >}}

To create the share but not immediately activate it, unset *Enable*. Click the *Save* button to create the share.

Unless the service is already running, the web interface prompts to enable the system service whenever a share is created.
Click the *ENABLE SERVICE* button to activate the service or click *Cancel* to keep the service inactive.

![WebdavServiceEnable](/images/SCALE/SharingCreateServiceEnable.png "WebDAV Service Activation from Share")

There are multiple ways to enter the edit mode for a share:
1. Click on the **WebDAV** header. From this page, click <i class="material-icons" aria-hidden="true" title="Expand">expand_more</i> then *Edit*.
2. Clicking anywhere within the row of the created share opens the **Edit WebDAV** section.

## Service Activation

To later enable or disable the WebDAV system service, go to either **System Settings > Services** and toggle *WebDAV*, or go to **Shares** and click <i class="material-icons" aria-hidden="true" title="Options">more_vert</i> within the **WebDAV** header and select *Turn Off Service*. To automatically start the service when TrueNAS boots, go to **System Settings > Services** and set *Start Automatically*.

To change or edit the WebDAV service settings, go to either **System Settings > Services** and click the <i class="material-icons" aria-hidden="true" title="edit">edit</i> or go to **Shares** and click <i class="material-icons" aria-hidden="true" title="Options">more_vert</i> within the **WebDAV** header and select *Config Service*.

![WebDAVServiceOptions](/images/SCALE/SharingWebdavServiceOptions.png "WebDAV Service Options")

For better data security, set the *Protocol* to *HTTPS*. This requires choosing an SSL certificate, but the *freenas_default* certificate is always available.
All of the *Protocol* options require defining a *Port* number. Make sure the WebDAV service port is not already used on the network.

To prevent unauthorized access to the shared data, set the *HTTP Authentication* to either *Basic* or *Digest* and create a new *Webdav Password*.

Be sure to click *Save* after making any changes.

## Connecting to the WebDAV Share

WebDAV shared data is accessible from a web browser.
To see the shared data, open a new browser tab and enter `{PROTOCOL}://{TRUENASIP}:{PORT}/{SHAREPATH}`.
Replace the elements in curly brackets `{}` with your chosen settings from the WebDAV share and service.
Example: `https://10.2.1.1:8081/mnt/corepool1/newdataset`

When the *Authentication* WebDAV service option is set to either *Basic* or *Digest*, a user name and password is required.
Enter the user name *webdav* and the password defined in the WebDAV service.
