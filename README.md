# apache-beam-runners

# Installation

- Make sure your K8s support ReadWriteMany storage. You can install NFS or Longhorn on K8s. Below are the optional steps to install Longhorn on the Kubernetes nodes
```
    sudo apt-get install open-iscsi nfs-common
    kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/master/deploy/longhorn.yaml
```
### You need custom image to include docker

- Edit the Dockerfile by including below step to install docker-ce. The editted file should look like the one in this repo
```
    RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-transport-https ca-certificates curl gnupg lsb-release && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    echo "deb [arch=amd64] https://download.docker.com/linux/debian bullseye stable" > /etc/apt/sources.list.d/docker.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends docker-ce && \
    apt-get purge -y --auto-remove lsb-release gnupg && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/* /usr/share/man /usr/share/doc /usr/share/doc-base /tmp/* /var/tmp/* && \
    find /var/lib/ -type f -name '*.log' -delete && \
    find /usr/share/locale -mindepth 1 -maxdepth 1 ! -name 'en*' | xargs rm -rf
```
- finally build and push the image to Docker Hub
```
    docker build . -t docker.io/<account>/your-custom-name-tag
    docker push  docker.io/<account>/your-custom-name-tag
```

# flink runner 

#### Documentation related to running Flink with K8s.

- https://beam.apache.org/blog/apache-beam-flink-and-kubernetes/

#### Check the documentation to create the image in the correct version compatible with Flink and Beam job

- https://beam.apache.org/documentation/runners/flink/#flink-version-compatibility

# spark runner 


