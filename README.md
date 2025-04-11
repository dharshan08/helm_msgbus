# create namespace
` kubectl create ns kafka`
# apply zookeeper
`helm install zookeeper oci://registry-1.docker.io/bitnamicharts/zookeeper -f zookeeper-values.yaml -n kafka`
# apply kafka
`helm upgrade --install kafka oci://registry-1.docker.io/bitnamicharts/kafka -f kafka-values.yaml -n kafka`
# apply configmap
`kubectl create configmap kafka-config --from-file=strimzi.properties=strimzi.properties -n kafka`
# apply redpanda
`helm upgrade --install my-console redpanda/console -f redpanda-values.yaml -n kafka`
# note to bound persistent volume claim
`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`
# verify pvc bound and installation
`kubectl get pods -n local-path-storage`
`kubectl get sc`
# apply minio
`helm install minio oci://registry-1.docker.io/bitnamicharts/minio -f minio-values.yaml -n kafka`


