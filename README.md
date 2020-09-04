#### Installation Instruction of Pi-Hole + VPN


------------

**Brief :**<br>
*Many Cloud Hosting providers don't allow an Open DNS Resolver. So turn your server in Pi-Hole and route traffic between the DNS server is not possible. Thus we are using OpenVpn and select its internal DNS server as Pi-Hole.*<br>

**Installation Instruction :**<br>

*I prefer to use Debian server in my Case that is Debian 9, But installation process on every linux will be quite similar.*<br><br>
*Please watch my YouTube video if you stuck :*<br><br>
[![Watch it on YouTube](https://firebasestorage.googleapis.com/v0/b/webtuhin.appspot.com/o/watch%20it%20on%20yt.png?alt=media&token=18a34920-8c94-471c-aa25-9bd8b1751ea6 "Watch it on YouTube")](https://youtu.be/UMQGYNEtJj8 "Watch it on YouTube")
<br><br><br>
*Login as **root*** <br>
*Firstly install OpenVpn and Configure it:*<br>
```bash
wget https://git.io/vpn -O openvpn-install.sh
chmod 755 openvpn-install.sh
./openvpn-install.sh
```
<br>

*Like This :*<br>

```bash
Welcome to this quick OpenVPN "road warrior" installer

I need to ask you a few questions before starting the setup
You can leave the default options and just press enter if you are ok with them

First I need to know the IPv4 address of the network interface you want OpenVPN
listening to.
IP address: [YOUR-PUBLIC-IP]

Which protocol do you want for OpenVPN connections?
   1) UDP (recommended)
   2) TCP
Protocol [1-2]: 1

What port do you want OpenVPN listening to?
Port: 1194

Which DNS do you want to use with the VPN?
   1) Current system resolvers
   2) Google
   3) OpenDNS
   4) NTT
   5) Hurricane Electric
   6) Verisign
DNS [1-6]: 1

Finally, tell me your name for the client certificate
Please, use one word only, no special characters
Client name: tuhin

Okay, that was all I needed. We are ready to setup your OpenVPN server now
Press any key to continue...
```

<br>*After OpenVpn Installed, install Pi-Hole :*<br>
```bash
curl -sSL https://install.pi-hole.net | bash
```
<br>

*Select **"tun0"**  as an Interface ,*<br>
*Everything will be Default ,*<br>
*Now you have to change the IP address :*<br>
```bash
##IP Address
10.8.0.1/24
```
<br>

*Gateway will be remaining same (Private IP of  Server) ,*<br>
*Everything will be Default  again,*<br>
*After Pi-Hole was installed ,*<br>
*Edit the OpenVPN config file :*<br>

```bash
nano /etc/openvpn/server/server.conf
```
<br>*Set this line to use your Pi-hole's IP address:* <br>

```bash
push "dhcp-option DNS 10.8.0.1"
```
<br>*Restart OpenVPN to apply the changes :* <br>

```bash
service openvpn-server@server restart
```

<br>*Installation Finished*<br><br>

**Connect with Pi-Hole**<br>
*To Generate a new Client*<br>
```bash
## Go To root directory and run the installation command again
./openvpn-install.sh
## Give option 1 and enter a name to generate a new user
```
<br>

*Send the "**.ovpn**" to web directory  to share the connection keys .*<br>
*Download  OpenVpn Connect in your devices and import the key to connect ,*<br>
<br>

[![Download Openvpn Client](https://firebasestorage.googleapis.com/v0/b/webtuhin.appspot.com/o/openvpn.png?alt=media&token=17dcec21-bfdf-49e2-8e6f-7c545c29984e "Download Openvpn Client")](https://openvpn.net/download-open-vpn/ "Download Openvpn Client")
<br><br>
### Thank You ❤
