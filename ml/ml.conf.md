## GPU conf
* zotac amp box mini 230w
* nvidia rtx 2060(inno3d 196mm)
* https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-19-04-disco-dingo-linux?fbclid=IwAR1n7AeQA0hQ5ELHln8xzWosWQ3e7KNEAh9ueEhN2om4YdODJXUud-yhxxY
    * ubuntu-drivers autoinstall OR apt install nvidia-driver-418
    * reboot
* https://devtalk.nvidia.com/default/topic/1061059/egpu-issue-how-to-enable-the-external-gpu-to-recognize-the-external-monitor-/?fbclid=IwAR0IF-GDdLj94jc0UUai50XcdQ3G5mKGIaMJi8tXZYTC6LY7dEwj1eLvTTM
    * vi /usr/share/X11/xorg.conf.d/10-nvidia.conf
    ```
    Section "OutputClass"
        Identifier "nvidia"
        MatchDriver "nvidia-drm"
        Driver "nvidia"
        Option "AllowEmptyInitialConfiguration"
        Option "AllowExternalGpus" "true"
        ModulePath "/usr/lib/x86_64-linux-gnu/nvidia-418/xorg"
    EndSection
    ```
* nvidia-smi


## unity, ml-agents
* unity hub
    * https://unity3d.com/kr/get-unity/update
    * https://moordev.tistory.com/299


## 미분류: TODO
* apt-get install python3-pip python3-dev

* pip3 install tensorflow-gpu

* 파이썬 과학 라이브러리: 넘파이, 싸이파이, 맷플롯립
    * apt-get install python3-numpy python3-scipy python3-matplotlib python3-yaml
* HDF5: 대용량 수치 데이터 파일을 이진 포맷으로 저장, 케라스 모델이 효율적으로 저장 
    * apt-get install libhdf5-serial-dev python3-h5py
* 케라스 모델 시각화: 필수 아님
    * apt-get graphviz
    * pip install pydot-ng
* apt-get install python3-opencv

* GPU
    * CUDA: https://developer.nvidia.com/cuda-downloads
    * cuDNN: https://developer.nvidia.com/cudnn
    
* 케라스
    * pip3 install keras



