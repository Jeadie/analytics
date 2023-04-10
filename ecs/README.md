
## Creating ECS Cluster
aws ecs create-capacity-provider \
    --name "t2micro-asg" \
    --auto-scaling-group-provider "autoScalingGroupArn=arn:aws:autoscaling:us-east-1:383495223751:autoScalingGroup:fced8cc2-2dfd-4c4d-a4ef-e9c0213a65ab:autoScalingGroupName/plausible"

aws ecs create-cluster --cluster-name plausible --capacity-providers arn:aws:ecs:us-east-1:383495223751:capacity-provider/t2micro-asg

## Setting up docker compose
docker context create ecs plausible-ecs
docker context use plausible-ecs


# Policy Document
https://docs.docker.com/cloud/ecs-integration/#requirements
aws iam create-policy --policy-name docker-ecs-policy  --policy-document file://policy_document.json
aws iam create-role --role-name docker-ecs --assume-role-policy-document file://ec2_trust_policy.json
aws iam attach-role-policy --role-name docker-ecs --policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/docker-ecs-policy

    
