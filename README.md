Setting Up a Firewall with `iptables`

Make the `firewall.sh` script executable and run it:

`chmod +x firewall.sh
sudo ./firewall.sh`

Setting Up OpenVPN

Install OpenVPN on your server. For Debian-based systems:

`sudo apt-get update
sudo apt-get install openvpn easy-rsa`

Configuration
Set Up the CA Directory:
`make-cadir ~/openvpn-ca
cd ~/openvpn-ca`

Update the `vars` file with your own information.

Build the Certificate Authority:
`source ./vars
./clean-all
./build-ca`

Generate Server Certificate and Key:
`./build-key-server server
./build-dh
openvpn --genkey --secret keys/ta.key`

Generate Client Certificates:
`./build-key client1`

Create the server configuration `file /etc/openvpn/server.conf`

Start the OpenVPN Service:
`sudo systemctl start openvpn@server
sudo systemctl enable openvpn@server`

