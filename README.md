Some relatively generic homelab setup that starts off super specific to a few goals...

# Goals
 
1. Relatively secure to have on home network
1. Able to host multiple services
    1. [ack-wire](https://github.com/nwself/ack-wire/)
    1. recipes of some kind
        * maybe still [tandoori](https://github.com/TandoorRecipes/recipes)? bc it's django? 
    1. media
        * plex (I already bought lifetime whatever from them. so i think they should play nice with the server?)
        * [jellyfin](https://jellyfin.org/) serving same files as plex? 
    1. [nextcloud](https://nextcloud.com/)
    1. [Solid](https://solidproject.org/) server
        * [lots of options](https://solidproject.org//self-hosting/css), but maybe it would make sense to start as a nextcloud add-on?

# Implementation
1. static ip from ISP
1. only reachable via wireguard (kinda vpn but better?)
    1. vnc
    1. ssh
1. docker something?
1. [dmz](#DMZ) to isolate publicly hosted things from other machines in the house

# QUESTIONS
1. are these the goals?
1. is the implementation above what we want?
1. is the DMZ impl below what we want?
1. devices
    1. where should security cams be??
        1. maybe make them require vpn? maybe can't because google/nest?
    1. august smart lock?
    1. webthings server?
    1. nest thermostat?


# Later

1. nathan's [notes thing](https://raneto.com/)?
1. open source ngrok?
    * e.g. service to help support reaching a service from outside that's behind nat and whatnot, possibly via [frp](https://github.com/fatedier/frp#accessing-internal-web-services-with-custom-domains-in-lan)?
1. [Automatic ripping machine](https://github.com/automatic-ripping-machine/automatic-ripping-machine)?

# DMZ

What even is this and how do I do it? 

## Hardware
1. eero B010001. which is maybe eeor pro 2nd gen (house wifi router hard wired into ISP provided "fiber modem" [ONT?])
1. linksys wrt3200acm (is it running openwrt rn?)
1. NUC Intel 11 Pro Kit NUC11TNKi3 Mini Desktop PC Computer - 11th Gen Intel Core i3-1115G4 up to 4.10 GHz Processor, 16GB DDR4 Memory, 512GB PCIe SSD, Intel UHD Graphics

## Implementation
so what if like:
1. fiber into house and into ONT
1. ONT <--> linksys (more features?) via ethernet
    * linksys runs [firewall and has rules to send outside traffic to dmz?](https://openwrt.org/docs/guide-user/firewall/fw3_configurations/fw3_dmz)
1. linksys <--> eero via ethernet
    1. eero <--> home and guests (or should guests be on linksys?) via wifi
    1. linksys <--> NUC via ethernet

