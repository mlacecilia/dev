* __\_\_hb_inetIfInfo( `[<lNoAliases>] [, <nAddrFamily>]` ) ➜ `<aInfo>`__   
`<lNoAliases>` is .F. by default so aliases are included   
`<nAddrFamily>` is HB_SOCKET_AF_INET by default   
`<aInfo>` is an array in which each entry is also array with the following fields:   
------|----|-----    
HB_SOCKET_IFINFO_FAMILY   | 1 |   address family   
HB_SOCKET_IFINFO_NAME     | 2 |   interface name   
HB_SOCKET_IFINFO_FLAGS    | 3 |   flags HB_SOCKET_IFF_*   
HB_SOCKET_IFINFO_ADDR     | 4 |   interface address   
HB_SOCKET_IFINFO_NETMASK  | 5 |   subnetmask   
HB_SOCKET_IFINFO_BROADCAST| 6 |   broadcast address   
HB_SOCKET_IFINFO_P2PADDR  | 7 |   point-to-point address   
HB_SOCKET_IFINFO_HWADDR   | 8 |   hardware address   
