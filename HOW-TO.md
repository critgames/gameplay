# Google Cloud Storage

## Manual Push
```
$ gsutil -m cp -r ./_site/* gs://gameplay.critgames.com
```

## Install
```
# Update the apt package index
sudo apt-get update

# Install dependencies
sudo apt-get install -y gnupg

# Add the gcsfuse package repository
echo "deb http://packages.cloud.google.com/apt gcsfuse-buster main" | sudo tee -a /etc/apt/sources.list.d/gcsfuse.list

# Import the public key for the repository
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

# Install gcsfuse
sudo apt-get update
sudo apt-get install gcsfuse
```

## Authenticate
```
# Authenticate using the default service account or any other service account key
gcloud auth activate-service-account --key-file=/mnt/disk/web/gameplay/key.json
```

## Mount
```
# Mount the GCS bucket
gcsfuse -o allow_other --implicit-dirs gameplay.critgames.com /mnt/disk/gameplay
```

## Unmount
```
fusermount -u /mnt/disk/gameplay
```

## Mount Automatically at boot
Add to /etc/fstab
```
gameplay.critgames.com /mnt/disk/gameplay gcsfuse rw,_netdev,allow_other,implicit_dirs,uid=1001,gid=33
```
