# kubernetes-vagrant

Master:
for SERVICES in etcd kube-apiserver kube-controller-manager kube-scheduler; do
	systemctl restart $SERVICES
	systemctl enable $SERVICES
	systemctl status $SERVICES
done

Minion:
for SERVICES in kube-proxy kubelet docker; do
    systemctl restart $SERVICES
    systemctl enable $SERVICES
    systemctl status $SERVICES
done
