# satip-rtp
This is an improved version of the `multicast-rtp` tool for controlling a SAT>IP server.

The original version is forked from the *satip-axe* project:
https://github.com/perexg/satip-axe/blob/master/tools/multicast-rtp

### Advantages of this version:
1. It accepts command line parameters (a configuration file isn't need, but still available).
2. Graceful exit (from Terminal & from scripts).
3. Shutdown of the streams (it sends the TEARDOWN RTSP message when closing).
4. Configurable target address (if the server accept it, for example minisatip does it).
5. Improved help.
6. Quiet mode for running as daemon.

### Examples:
- It uses the SAT>IP at address 192.168.1.100 to streaming KIKA-HD from 19.2E to the multicast 239.0.0.1:10000: `multicast-rtp -s 192.168.1.100:554 -d 239.0.0.1 -p 10000 -u "src=1&freq=11347&pol=v&ro=0.35&msys=dvbs2&mtype=8psk&plts=on&sr=22000&fec=23&pids=0,17,18,6600,6610,6620,6630"`
- Run as the original *satip-axe* tool: `multicast-rtp -s 127.0.0.1:554 -c /etc/sysconfig/multicast`
  
### Notes:
- If your server doesn't support spoofing of the "target" address then you can only unicast to the same device where you run this tool.
- When the server doesn't support a multicast address as "unicast", then you can't use it for setting the target multicast address. The port is selectable anyway, but the stream is streamed to the multicast address assigned in the SAT>IP server.
- You can use this tool to manage from scripts any SAT>IP server if the client (receiver) accepts multicast TS inputs (or unicast when running in the same server). The streaming will be open until you stop the tool.
