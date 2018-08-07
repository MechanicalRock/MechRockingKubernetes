# Mech Rocking Kubernetes

## Requirements
1. Python3 Installed

## Setup Instructions

1. Set up required environment variables:
    1. `export PROFILE=<<name of aws profile>>`
1. `aws cloudformation deploy --template-file IAM.yaml --stack-name eksServiceRole --capabilities CAPABILITY_NAMED_IAM --profile ${PROFILE}`
1. `aws cloudformation deploy --template-file VPC.yaml --stack-name eksVPC --capabilities CAPABILITY_IAM --profile ${PROFILE}`
1. `aws cloudformation deploy --template-file cluster.yaml --stack-name eksCluster --profile ${PROFILE}`
1. `aws cloudformation deploy --template-file nodes.yaml --stack-name eksNodes --capabilities CAPABILITY_IAM --profile ${PROFILE}`
1. Install `eks-switcher`
    1. For MacOS `pip3 install eks-switcher`
1. Run `eks-switcher --profile ${PROFILE}`
1. Get the NodeInstanceRole Output from the `eksNodes` stack and paste it into the `node-config-map.yaml` file
1. Run `kubectl apply -f ./node-config-map.yaml`
1. Run `kubectl get nodes --watch` until the nodes appear `ready`
