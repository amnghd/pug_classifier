
GPU
===
Create a GPU instance:

```
docker-machine create --driver amazonec2 --amazonec2-access-key --amazonec2-secret-key --amazonec2-root-size 100 --amazonec2-zone b --amazonec2-vpc-id --amazonec2-subnet-id --amazonec2-instance-type g2.2xlarge --amazonec2-private-address-only --amazonec2-ami ami-76b2a71e awsgpunotebook
```

SSH in:

```
docker-machine ssh awsnotebook
```

Setup the GPU following the instructions here: https://github.com/mdagost/MScA_code/blob/master/lecture_08/bootstrap_aws_gpu.sh

Install `nvidia-docker` like so:

```
git clone https://github.com/NVIDIA/nvidia-docker
cd nvidia-docker
sudo make install
```

Get our software:

```
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
git lfs install
git clone https://github.com/mdagost/pug_classifier.git
cd pug_classifier
git lfs pull
```

Run the container:

```
sudo nvidia-docker run -d -p 8888:8888 mdagost/pug_classifier_gpu_notebook
```
