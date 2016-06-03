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





## Các ghi chép khác

- Tùy chọn đầu ra cho máy ảo kéo từ ESXi về
```sh
- Cú pháp 
`-os qcow2 -o libvirt`

- Ví dụ: 
virt-v2v -ic esx://172.17.77.150/?no_verify=1 -os qcow2 -o libvirt -os congvirtimages cong-centos65 
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


- Kiểm tra thông tin của VM trên VCENTER

```sh
- Lệnh: 

virsh -c 'vpx://administrator%40vsphere.local@172.17.77.149/MDT/172.17.77.150?no_verify=1' dumpxml "cong-centos65"
Enter administrator@vsphere.local's password for 172.17.77.149:


- Kết quả: 

<domain type='vmware'>
  <name>cong-centos65</name>
  <uuid>564db5ec-7ad8-0c76-a18c-d138f00db89b</uuid>
  <memory unit='KiB'>2097152</memory>
  <currentMemory unit='KiB'>2097152</currentMemory>
  <vcpu placement='static'>2</vcpu>
  <os>
    <type arch='x86_64'>hvm</type>
  </os>
  <clock offset='utc'/>
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
  <devices>
    <disk type='file' device='disk'>
      <source file='[datastore1] cong-centos65/cong-centos65.vmdk'/>
      <target dev='sda' bus='scsi'/>
      <address type='drive' controller='0' bus='0' target='0' unit='0'/>
    </disk>
    <disk type='file' device='cdrom'>
      <source file='[datastore1] ISO/CentOS-6.5-x86_64-minimal.iso'/>
      <target dev='hdc' bus='ide'/>
      <address type='drive' controller='0' bus='1' target='0' unit='0'/>
    </disk>
    <controller type='scsi' index='0' model='lsilogic'/>
    <controller type='ide' index='0'/>
    <interface type='bridge'>
      <mac address='00:0c:29:0d:b8:9b'/>
      <source bridge='VM Network'/>
      <model type='vmxnet3'/>
    </interface>
    <interface type='bridge'>
      <mac address='00:0c:29:0d:b8:a5'/>
      <source bridge='VMNAT'/>
      <model type='vmxnet3'/>
    </interface>
    <video>
      <model type='vmvga' vram='4096'/>
    </video>
  </devices>
</domain>

```



## Tham khảo
```sh
1. http://yazpik.github.io/blog/2014/12/15/virtual-machine-migration-from-vmware-to-openstack/
2. ..
```