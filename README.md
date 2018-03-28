* __\_\_hb_inetIfInfo( `[<lNoAliases>] [, <nAddrFamily>]` ) ➜ `<aInfo>`__   
`<lNoAliases>` is .F. by default so aliases are included   
`<nAddrFamily>` is HB_SOCKET_AF_INET by default   
`<aInfo>` is an array in which each entry is also array with the following fields:   
   
Defined constant (hbsocket.ch) | # | Returned value         
-----------------------------|---|---------------------
HB_SOCKET_IFINFO_FAMILY   | 1 |   address family   
HB_SOCKET_IFINFO_NAME     | 2 |   interface name   
HB_SOCKET_IFINFO_FLAGS    | 3 |   flags HB_SOCKET_IFF_*   
HB_SOCKET_IFINFO_ADDR     | 4 |   interface address   
HB_SOCKET_IFINFO_NETMASK  | 5 |   subnetmask   
HB_SOCKET_IFINFO_BROADCAST| 6 |   broadcast address   
HB_SOCKET_IFINFO_P2PADDR  | 7 |   point-to-point address   
HB_SOCKET_IFINFO_HWADDR   | 8 |   hardware address   

* __hb\_inetCompress( `<pSocket>, [<nCompressionLevel>], [<nStrategy>], [<cPass>] )` ) ➜ `NIL`__  
      which enables ZLIB compression for given HB_INET*() socket.
      <pSocket> is a socket created by one of HB_INET*() functions
      <nCompressionLevel> is compression factor between 1 (fastest) and
                          9 (best) (see HB_ZLIB_COMPRESSION_*)
                          0 (none) disable compression on output data
                          but decompression is still working.
      <nStrategy> is used to tune compression algorithm,
                  see HB_ZLIB_STRATEGY_*
      The compression must be enabled on both connection sides, i.e.
      on the server side:
         conn := hb_inetAccept( sock )
         hb_inetCompress( conn )
      and on the client side:
         sock := hb_inetConnect( cServer, nPort )
         hb_inetCompress( sock )
      in the same moment but it's not necessary to enable it at the
      beginning of connection. It can be done later, i.e. when both
      sides agree to enable connection using some custom protocol.
      The compression has effect only on stream connections, i.e.
      TCP and it's ignored in datagram connections like UDP.
      This function can be executed more then once changing the compression
      parameters but it causes that all data in readahead decompression
      buffer is discarded. When called with HB_ZLIB_COMPRESSION_DISABLE
      as <nCompressionLevel> then support for stream compression is removed
      and sockets works again in raw mode.
      The compression level and strategy do not have to be the same on both
      connection sides. Each side can chose the best settings for data it's
      going to send.

      This code was written in a way which allows to easy implement
      alternative compression methods or other extensions like encryption
      in existing HB_INET*() sockets also by non core code. The public C
      functions declared in hbznet.h allows to use this extension with raw
      harbour sockets two.
