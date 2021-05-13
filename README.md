# lv-architecture-interface

(based from LabVIEW 2015)

This repo contains incredibly basic templates/examples for NRE (non re-entrant) and RE (re-entrant) interfaces. It's meant to be copied and pasted with functionality added in after the fact. 

As a **disclaimer**, these support __basic__ functionality, although I do think it's pretty extensible to handle most UIs, I think if you want to implement sub panels or desire communication between between different interfaces, you'll hit the limits of this architecture and will need to make modifications.

## lv-interface-nre

This is a simple template for a non re-entrant interface developed for high concurrency (i.e. a lot is happening simultaneously). It's also meant to be fairly scalable within its context.

For more information, check out [README.md](./source/lv-interface-nre/README.md)

## lv-interface-re

This is another template for a re-entrant interface, it's identical to the non re-entrant example except that it's configured for re-entrancy. The launcher.vi can start mujltiple instances of the main.

For more information, check out the [README.md](./source/lv-interface/re/README.md)
