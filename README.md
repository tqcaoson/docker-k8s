# khởi tạo một Cluster
kubeadm init --apiserver-advertise-address=172.16.10.100 --pod-network-cidr=192.168.0.0/16

# Cài đặt giao diện mạng calico sử dụng bởi các Pod
kubectl apply -f https://docs.projectcalico.org/v3.23/manifests/calico.yaml

# Thông tin cluster
kubectl cluster-info

# Các node (máy) trong cluster
kubectl get nodes

# Các pod (chứa container) đang chạy trong tất cả các namespace
kubectl get pods -A

# Xem nội dung cấu hình hiện tại của kubectl
kubectl config view

# Thiết lập file cấu hình kubectl sử dụng cho 1 phiên làm việc hiện tại của termianl
export KUBECONFIG=/Users/xuanthulab/.kube/config-mycluster

# Gộp file cấu hình kubectl
export KUBECONFIG=~/.kube/config:~/.kube/config-mycluster
kubectl config view --flatten > ~/.kube/config_temp
mv ~/.kube/config_temp ~/.kube/config

# Các ngữ cảnh hiện có trong config
kubectl config get-contexts

# Đổi ngữ cảnh làm việc (kết nối đến cluster nào)
kubectl config use-context kubernetes-admin@kubernetes

# Lấy mã kết nối vào Cluster
kubeadm token create --print-join-command

# node worker kết nối vào Cluster
kubeadm join 172.16.10.100:6443 --token 5ajhhs.atikwelbpr0 ...