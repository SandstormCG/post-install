NOTE: This is a merge between some different ansible project into just a cleaner and improved one, so it still is missing testing.

# Steps to install

Tras instalar aplicar los shortcuts de kde (.kksrc en la carpeta config/files)

On desktop systems `systemctl start sshd` to execute the playbook from another computer, and stop it after install.


### VM Config (Single GPU-Passthrough qemu-kvm)

Configure IIOMU on the system after install to be able to do single GPU passthrough 

`sudo nano /etc/default/grub`

AMD:
FIND the line - GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
CHANGE it to - GRUB_CMDLINE_LINUX_DEFAULT="amd_iommu=on iommu=pt iommu=1 video=efifb:off quiet splash"

INTEL:
FIND the line - GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
CHANGE it to - GRUB_CMDLINE_LINUX_DEFAULT="intel_iommu=on iommu=pt iommu=1 video=efifb:off quiet splash"

`sudo update-grub`(Other distros not yet implemented) or `sudo grub-mkconfig -o /boot/grub/grub.cfg`(Arch)


### Fix some library errors for 32bit games

After installing steam proton create soft link for libssl.so.1.0.0 and libcrypt.so.1.0.0 as some gog games still use this old libraries, and arent already on repos ( (Source)[https://www.reddit.com/r/baldursgate/comments/qi1z0h/baldurs_gate_ee_on_linux_libsslso100/] ).
please ln -s ~/.steam/bin/steam-runtime/lib/i386-linux-gnu/libssl.so.1.0.0 /usr/lib/libssl.so.1.0.0\
please ln -s ~/.steam/bin/steam-runtime/lib/i386-linux-gnu/libcrypto.so.1.0.0 /usr/lib/libcrypto.so.1.0.0




IIRC: 
library/yay (source)[https://github.com/mnussbaum/ansible-yay]
qemu--> hooks (for single GPU-passthrough) (source)[https://gitlab.com/risingprismtv/single-gpu-passthrough]