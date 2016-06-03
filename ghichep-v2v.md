# Các ghi chép về tool v2v

- Khai báo file .netnc
```sh
machine IP_ESXi login root password mat_khau
```

- Phân quyền 
```sh
chmod 600 .netnc
```

- Kết nối tới ESX để kéo máy ảo về
```sh
virt-v2v -ic esx://172.17.77.150/?no_verify=1 -o libvirt -os congvirtimages Cong-u1401_clone
```

- Kiểm tra các máy trên esx
```sh
virsh -c esx://172.17.77.150/?no_verify=1 list --all
```
