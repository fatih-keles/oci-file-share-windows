## Prerequisities 
1. Install oci cli as described [here](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/cliinstall.htm)  and get it working 
2. Install [WinFsp](https://winfsp.dev/rel/)
3. Download [rclone](https://rclone.org/downloads/), unzip and put on your PATH. 
4. Configure as described [here](https://rclone.org/oracleobjectstorage/)

```bash 
 rclone config
```
You should see something like this:
```bash
Configuration complete.
Options:
- type: oracleobjectstorage
- provider: user_principal_auth
- namespace: <redacted>
- compartment: <redacted>
- region: uk-london-1
Keep this "remote" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y

Current remotes:

Name                 Type
====                 ====
remote               oracleobjectstorage
```

## Usage 
All commands are listed [here](https://rclone.org/oracleobjectstorage/)

Assuming you named your remote as `remote`, 

- See all buckets:
```
$ rclone lsd remote:
          -1 2022-11-04 14:37:34        -1 a2b-online
          -1 2022-10-03 17:02:31        -1 adb_backups
          -1 2022-10-03 21:57:18        -1 auto-blur-images
          -1 2022-07-15 15:23:06        -1 db-related
          -1 2022-07-29 13:18:04        -1 eexp-demo-backups
          -1 2022-08-24 13:24:05        -1 my_jar_files
          -1 2022-08-12 11:17:01        -1 oci-logs._flowlogs.ocid1.compartment.oc1..aaaaaaaapbatjdpgcbfpvwxmfkav5ijagbf7aepp5ln7xxlpl5ba347xukja
          -1 2022-10-08 21:45:05        -1 ocr-documents
          -1 2022-10-10 17:49:23        -1 ocr-documents-temp
          -1 2022-10-08 22:36:27        -1 ocr-extracts
          -1 2023-03-29 14:43:17        -1 rclone-test
          -1 2022-10-05 22:31:06        -1 vmdk
```

- Create a new bucket:
```bash
rclone mkdir remote:bucket
```

- List the contents of a bucket:
```bash 
rclone ls remote:bucket
```

- Mount remote as a drive S:
```bash
rclone mount remote: S:
```

- Mount remote as a folder in your home directory:
```bash
rclone mount remote: ~/rclone-test
```

- Copy local file `CSA.PNG` to remote bucket:
```bash 
rclone copy CSA.PNG remote:rclone-test
```