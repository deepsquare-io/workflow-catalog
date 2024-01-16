# Counter-Strike 2 server

## Usage

The server need multiple manual steps, including a wireguard server and interacting with an interactive session.

1. Setup a [wireguard server](https://docs.deepsquare.run/workflow/guides/connecting-wireguard) and forward the CS2 ports (27015 and 27016 UDP and TCP). Example of wireguard config:

   ```shell
   [Interface]
   Address = 10.0.0.1/24, fd00:1234:5678::1/64
   ListenPort = 51820
   PrivateKey = <TO BE FILLED>

   [Interface]
   PostUp = nft add rule ip wireguard prerouting udp dport 27015 dnat to 10.0.0.4/32
   PostUp = nft add rule ip wireguard prerouting tcp dport 27015 dnat to 10.0.0.4/32
   PostUp = nft add rule ip wireguard prerouting udp dport 27016 dnat to 10.0.0.4/32
   PostUp = nft add rule ip wireguard prerouting tcp dport 27016 dnat to 10.0.0.4/32
   PostUp = nft add rule ip6 wireguard prerouting udp dport 27015 dnat to fd00:1234:5678::4/128
   PostUp = nft add rule ip6 wireguard prerouting tcp dport 27015 dnat to fd00:1234:5678::4/128
   PostUp = nft add rule ip6 wireguard prerouting udp dport 27016 dnat to fd00:1234:5678::4/128
   PostUp = nft add rule ip6 wireguard prerouting tcp dport 27016 dnat to fd00:1234:5678::4/128

   # cs2
   [Peer]
   PublicKey = <TO BE FILLED>
   AllowedIPs = 10.0.0.4/32,  fd00:1234:5678::4/12
   ```

2. Fill the missing fields in the `cs2.yaml` file.
3. Submit the job. The job will output a `bore.deepsquare.run` URL. Use this URL to fill the 2FA code.
4. Wait for the second step. The job will output an other `bore.deepsquare.run` URL. Use this URL to interact with the server.
