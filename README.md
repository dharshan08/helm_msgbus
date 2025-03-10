# create namespace
` kubectl create ns kafka`
# apply zookeeper
`helm install zookeeper oci://registry-1.docker.io/bitnamicharts/zookeeper -f zookeeper-values.yaml -n kafka`
