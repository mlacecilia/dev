* __hb\_inetCompress( `<pSocket>, [<nCompressionLevel>], [<nStrategy>], [<cPass>] )` ) ➜ `NIL`__  
      enables ZLIB compression for given HB\_INET*() socket.   
      `<pSocket>` is a socket created by one of HB\_INET*() functions      
      `<nCompressionLevel>` is compression factor between 1 (fastest) and 9 (best) (see HB\_ZLIB\_COMPRESSION\_*) 0 (none) disable compression on output data but decompression is still working.   
      `<nStrategy>` is used to tune compression algorithm, see HB\_ZLIB\_STRATEGY\_\*   
      The compression must be enabled on both connection sides, i.e.   
      on the server side:
          
         conn := hb_inetAccept( sock )       
         hb_inetCompress( conn )
          
      and on the client side:
          
         sock := hb_inetConnect( cServer, nPort )       
         hb_inetCompress( sock )    
         
      in the same moment but it's not necessary to enable it at the beginning of connection. It can be done later, i.e. when both sides agree to enable connection using some custom protocol.   
      The compression has effect only on stream connections, i.e. TCP and it's ignored in datagram connections like UDP.   
      This function can be executed more then once changing the compression parameters but it causes that all data in readahead decompression buffer is discarded.    
When called with HB_ZLIB_COMPRESSION_DISABLE as `<nCompressionLevel>` then support for stream compression is removed and sockets works again in raw mode.
      The compression level and strategy do not have to be the same on both connection sides. Each side can chose the best settings for data it's going to send.
      This code was written in a way which allows to easy implement alternative compression methods or other extensions like encryption
      in existing HB\_INET*() sockets also by non core code. The public C functions declared in hbznet.h allows to use this extension with raw harbour sockets two.
