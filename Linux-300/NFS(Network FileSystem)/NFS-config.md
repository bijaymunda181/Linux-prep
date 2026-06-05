## Server Side Configuration
1. **Install NFS packages**</br>
   sudo yum install -y nfs-utils</br>
2. **Create a shared directory**</br>
   sudo mkdir -p /mnt/nfs-share</br>
3. **Configure NFS exports**</br>
   Edit the exports file:</br>
   sudo vi /etc/exports</br>
**Add:**</br>
   /mnt/nfs-share 192.168.100.165(rw,sync,no_root_squash)</br>
   - rw = Read/Write access
   - sync = Write data immediately
   - no_root_squash = Client root user remains root on the NFS share
4. **Start and enable NFS services**</br>
   sudo systemctl enable rpcbind</br>
   sudo systemctl enable nfs-server</br>
**Verify:**</br>
   sudo systemctl status nfs-server </br>
5. **Apply export configuration**</br>
   sudo exportfs -rav</br>
**Check exports:**</br>
   sudo exportfs -v</br>
6. **Configure firewall**</br>
   sudo firewall-cmd --permanent --add-service=nfs</br>
   sudo firewall-cmd --permanent --add-service=mountd</br>
   sudo firewall-cmd --permanent --add-service=rpc-bind</br>
   sudo firewall-cmd --reload</br>
7. **Verify NFS share**</br>
   showmount -e localhost</br>
**Expected output:**</br>
   Export list for localhost</br>
   /nfs-share 192.168.100.165 </br>

## NFS Client Configuration
1. **Install NFS client package**</br>
   sudo yum install -y nfs-utils</br>
2. **Create mount point**</br>
   sudo mkdir /mnt/nfs</br>
3. **Mount NFS share**</br>
   sudo mount -t nfs 192.168.100.163:/mnt/nfs-share /mnt/nfs</br>
4. **Verify**</br>
   df -h</br>
5. **Permanent Mount**</br>
**Edit:**</br>
   sudo vi /etc/fstab</br>
**Add:**</br>
   192.168.1.10:/nfs-share /mnt/nfs nfs defaults,_netdev 0 0