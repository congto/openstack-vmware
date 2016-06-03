# Các ghi chép về tool v2v


### Các bước cài đặt virsh-v2v
- Mô hình

```sh
update mô hình
```

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
# Kết nối thẳng tới ESX (không phải VCENTER)

virsh -c esx://172.17.77.150/?no_verify=1 list --all

http://prntscr.com/bbpjw1

# ?no_verify=1 : tùy chọn giúp không cần xác nhận SSL khi login vào ESX
```


## Các ghi chép khác

