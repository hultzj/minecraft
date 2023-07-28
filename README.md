# minecraft
1. Create new project minecraft-server
2. oc new-app --name hub itzg/minecraft-server -e EULA=TRUE
2. oc new-app --name=smp -e EULA=true itzg/minecraft-server
4. oc set env deploy smp TYPE=PAPER 
5. oc set env deploy hub TYPE=PAPER
6. oc new-app --name bungee itzg/bungeecord
7. Create hub pvc 
8. oc set volume deploy hub --add --name=hub-volume-1 -t pvc --claim-name=hubclaim 
   oc set volume deploy smp --add --name=smp-volume-1 -t pvc --claim-name=smpclaim --overwrite
   oc set volume deploy smp --add --name=smp-volume-1 -t pvc --claim-name=smpclaim --overwrite
# If you aren't doing local PV or NFS and have ODF/EBS backends then you only have to set PVC and don't touch PV.
    Do this for bungee and smp
9. Modify sed -i 's/online-mode=true/online-mode=false/' server.properties
10. Modify config file with nano on bungee
11. Loadbalancer only useful if you are manually setting it. 


NodePort and Loadbalancer configs are lies. Bungee is just going over the default port




Turn off ip forwarding in bungee config
turn off enforce secure profile to false on hub/smp 

If you go directly to the server without bungee it works. Port forwarding doesn't seem to be correct but instead the loadbalancer takes the target port vs the forwarding one. 

The created loadbalancer has to added to the dns zone


