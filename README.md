# aws_ec2_spot
This repository contains all the code related to EC2 Spot

https://aws.amazon.com/blogs/machine-learning/train-deep-learning-models-on-gpus-using-amazon-ec2-spot-instances/

Shell commands

aws ec2 run-instances \
    --image-id ami-0027dfad6168539c7 \
    --security-group-ids <SECURITY_GROUP_ID> \
    --count 1 \
    --instance-type m4.xlarge \
    --key-name <KEYPAIR_NAME> \
    --subnet-id <SUBNET_ID> \
    --query "Instances[0].InstanceId"
    

aws ec2 create-volume \
    --size 100 \
    --region <AWS_REGION> \
    --availability-zone <INSTANCE_AZ> \
    --volume-type gp2 \
    --tag-specifications 'ResourceType=volume,Tags=[{Key=Name,Value=DL-datasets-checkpoints}]' 

aws ec2 attach-volume \
    --volume-id vol-<your_volume_id> \
    --instance-id i-<your_instance_id> \
    --device /dev/sdf
        
        
sudo mkdir /dltraining
sudo mkfs -t xfs /dev/xvdf
sudo mount /dev/xvdf /dltraining
sudo chown -R ubuntu: /dltraining/
cd /dltraining
mkdir datasets
mkdir checkpoints        


aws ec2 terminate-instances \
    --instance-ids i-<your_instance_id> \
    --output text
    
    
