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