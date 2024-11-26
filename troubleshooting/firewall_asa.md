Esta solución lo encontré en el foro de GNS3, por defecto la consola de asa inicia en vnc, si intento hacerlo con telnet surgen problemas, esta es la solución para iniciar desde telnet.

    copy disk0:/coredumpinfo/coredump.cfg disk0:/use_ttyS0
    wr
    copy startup-config disk0:/startup-config
    conf t
    boot config disk0:/startup-config
    hostname ASAv951
    wr
    copy running-config disk0:/startup-config
    reload

    Then right click ASA and configure console type back to Telnet and startup output will eventually appear on putty console.
    Have hooked up ASDM ..all working good :-)

    You can make it persistent.  Click "edit->preferences->qemu VMs", highlight your ASAv VM, and click edit.  What you want to do, is to uncheck the box on the Advanced settings tab, that says "use this as a linked VM".  Hit apply, ok, etc...  
    Drop an instance of ASAv into a blank topology, do the procedure to enable serial access, and confirm it.  
     
    Before you make any other changes, shut down that VM, go back to edit->preferences, etc...  and re-check that "use as a linked VM" box, as well as changing the console to telnet.
    From that point on, all future instances you use of that ASAv VM, will have serial access enabled. 

[asav_not_booting](https://www.gns3.com/community/featured/asav-not-booting-correctly)
