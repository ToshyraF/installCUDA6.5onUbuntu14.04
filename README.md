# Step install CUDA6.5 on Ubuntu14.04

 	*** Before install cuda ,please close secure boot in bios ***
	
	How to check nvidia support
  
	lspci | grep -i nvidia
			
# 1.install dependencies
	sudo apt-get -y install gcc g++ build-essential automake linux-headers-$(uname -r) git gawk libcurl4-openssl-dev libjansson-dev xorg libc++-dev libgmp-dev python-dev

# 2.Disable nouveau
    2.1 nano /etc/modprobe.d/blacklist-nouveau.conf
		
    2.2 add these lines to it
      2.2.1 blacklist nouveau
      2.2.2 blacklist lbm-nouveau
      2.2.3 options nouveau modeset=0
      2.2.4 alias nouveau off
      2.2.5 alias lbm-nouveau off
		 
    2.3 echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
		
    2.4 sudo update-initramfs -u
		
    2.5 reboot
		
# 3.Install the nvidia display driver
    3.1 Dowloads driver nvidia graphic
    3.2 press ctrl + alt + f1 and insert user password
    3.3 sudo service lightdm stop
    3.4 go to path dowloads graphic nvidia and sudo chmod +x NVIDIA-Linux-x86_64-352.41.run
    3.5 sudo ./NVIDIA-Linux-x86_64-352.41.run --no-opengl-files
    3.6 check nvidia-smi
    3.7 sudo service lightdm start
		
# 4.install cuda
    4.1 cd && wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/cuda-repo-ubuntu1404_6.5-14_amd64.deb
    4.2 sudo dpkg -i cuda-repo-ubuntu1404_6.5-14_amd64.deb
    4.3 sudo apt-get update
    4.4 sudo apt-get -y install cuda-toolkit-6-5
    4.5 sudo usermod -a -G video $USER
    4.6 echo "" >> ~/.bashrc
    4.7 echo "export PATH=/usr/local/cuda-6.5/bin:$PATH" >> ~/.bashrc
    4.8 echo "export LD_LIBRARY_PATH=/usr/local/cuda-6.5/lib64:$LD_LIBRARY_PATH" >> ~/.bashrc
		
# 5.reboot

