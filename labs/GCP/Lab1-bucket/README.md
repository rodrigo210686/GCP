Create a Cloud Storage bucket using the gsutil command line
All Cloud Storage bucket names must be globally unique. To ensure that your bucket name is unique, these instructions will guide you to give your bucket the same name as your Cloud Platform project ID, which is also globally unique.

Cloud Storage buckets can be associated with either a region or a multi-region location: US, EU, or ASIA. In this activity, you associate your bucket with the multi-region closest to the region and zone that Qwiklabs or your instructor assigned you to.

On the Google Cloud Platform menu, click Activate Cloud Shell Activate Cloud Shell icon. If a dialog box appears, click Continue.

For convenience, enter your chosen location into an environment variable called LOCATION. Enter one of these commands:
```sh
export LOCATION=US
Copied!
Or

export LOCATION=EU
Copied!
Or

export LOCATION=ASIA
Copied!

```
```sh
In Cloud Shell, the DEVSHELL_PROJECT_ID environment variable contains your project ID. Enter this command to make a bucket named after your project ID:

gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID
```
Modify the Access Control List of the object you just created so that it is readable by everyone:
```sh
gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
```
