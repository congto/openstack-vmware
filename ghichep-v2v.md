# Các ghi chép về tool v2v


### Các bước cài đặt virsh-v2v
- Mô hình
```sh
update mô hình vào đây ....
```

- Môi trường cài đặt
```sh
update môi trường cài đặt vào đây ....
```

- Khai báo file .netnc
```sh
machine IP_ESXi login root password mat_khau
```

- Phân quyền 
```sh
chmod 600 .netnc
```

- Cài đặt virt-v2v
```sh
yum -y install qemu-kvm libvirt python-virtinst bridge-utils

yum install virt-v2v
```

- Tạo pool cho KVM


```sh
- Tạo file pool.xml

<pool type="dir">
        <name>virtimages</name>
        <target>
          <path>/home/images</path>
        </target>
</pool>

- Sử dụng lệnh virsh tạo pool

virsh pool-create --file pool.xml

- Kiểm tra pool vừa tạo

virsh pool-list

```

- Kết nối tới ESX để kéo máy ảo về
```sh
virt-v2v -ic esx://172.17.77.150/?no_verify=1 -o libvirt -os congvirtimages Cong-u1401_clone
```

- Kiểm tra các máy trên esx
```sh
# Kết nối thẳng tới ESX (không phải VCENTER)

virsh -c esx://172.17.77.150/?no_verify=1 list --all

# Tham khảo http://prntscr.com/bbpjw1

# Kết nối tới VCENTER

virsh -c 'vpx://administrator%40vsphere.local@172.17.77.149/MDT/172.17.77.150?no_verify=1' list --all

# Tham khảo: http://prntscr.com/bbpro7

# Nếu user của VCENTER có dạng `administrator@vsphere.local` thì phải sử dụng %40 vì 40 là mã ASCII của @. If the username contains a backslash (eg. DOMAIN\USER) then you will need to URI-escape that character using %5c: DOMAIN%5cUSER (5c is the hexadecimal ASCII code for backslash.) Other punctuation may also have to be escaped. Tham khảo :  http://prntscr.com/bbpv0a

# ?no_verify=1 : tùy chọn giúp không cần xác nhận SSL khi login vào ESX
```

## Các ghi chép khác



## Tham khảo
```sh
1. http://yazpik.github.io/blog/2014/12/15/virtual-machine-migration-from-vmware-to-openstack/
2. ..
```