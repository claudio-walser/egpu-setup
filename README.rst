Guide to get your egpu working in linux
=======================================
This is a very small guide of what I did to setup my egpu.

**My hardware**
- eGPU Enclosure: Razer Core X Chroma
- eGPU: Asus Geforce 1080 Strix TI with 11GB Ram
- Notebook: Lenovo X1 Extreme (already has a Intel HD Chip and a Nvidia Geforce 1050 TI Mobile)

**MySoftware**
- Fedora Silverblue 31
- akmod-nvidia and xorg-x11-drv-nvidia-cuda


PreConditions
#############
- setup the appropriate driver for the gpu's you are using
- ensure thunderbolt authorization works properly
- you should understand basic linux things, for example bash or systemd

Setup
#####
You only need to put 4 files at the right locations and you are basically done.

- https://raw.githubusercontent.com/claudio-walser/egpu-setup/master/egpu to /usr/local/bin/egpu
- https://raw.githubusercontent.com/claudio-walser/egpu-setup/master/egpu.service to /etc/systemd/system/egpu.service
- https://raw.githubusercontent.com/claudio-walser/egpu-setup/master/xorg.conf.egpu to /etc/X11/xorg.conf.egpu
- https://raw.githubusercontent.com/claudio-walser/egpu-setup/master/xorg.conf.internal to /etc/X11/xorg.conf.internal

Then run some commands

.. code-block:: bash

    # make the file executable
    sudo chmod +x /usr/local/bin/egpu

    # enable egpu.service
    sudo systemctl daemon-reload
    sudo systemctl enable egpu.service

You are done
############
If both of your xorg config files are right, you should now be able to switch to your egpu using:
/usr/local/bin/egpu start

Attention
#########
These are my configs, the might not work for you.
- **xorg.conf.internal** should basically contain what you had before you started using an egpu
- **xorg.conf.egpu** file could be useful for you, find out the Device ID with
    .. code-block:: bash
        lspci | grep VGA
        nvidia-smi -L # in case you have nvidia gpus as i do
