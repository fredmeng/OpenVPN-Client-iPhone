# OpenVPN-Client-iPhone

<p>This is about how to set up the OpenVPN client on your iPhone with step-by-step instructions.</p>

<p><br>Step 1: Install <b>OpenVPN Connect by OpenVPN</b> from App Store</p>

<p><br>Step 2: Find following 3 files on your OpenVPN server and scp to your mac.</p>

<pre>
/etc/easy-rsa/easyrsa3/pki/ca.crt
/etc/easy-rsa/easyrsa3/pki/issued/ios.crt
/etc/easy-rsa/easyrsa3/pki/private/ios.key
</pre>

<p><br>Step 3: Create an OpenVPN client config file e.g. <b>ios.ovpn</b> on your mac. Following is an example.</p>

<pre>
# Specify that we are a client and that we
# will be pulling certain config file directives
# from the server.
client

# Use the same setting as you are using on
# the server.
# On most systems, the VPN will not function
# unless you partially or fully disable
# the firewall for the TUN/TAP interface.
;dev tap
dev tun

# Windows needs the TAP-Windows adapter name
# from the Network Connections panel
# if you have more than one.  On XP SP2,
# you may need to disable the firewall
# for the TAP adapter.
;dev-node MyTap

# Are we connecting to a TCP or
# UDP server?  Use the same setting as
# on the server.
proto udp4

# The hostname/IP and port of the server.
# You can have multiple remote entries
# to load balance between the servers.
remote ec2-1-2-3-4.x.compute.amazonaws.com 1194

# Choose a random host from the remote
# list for load-balancing.  Otherwise
# try hosts in the order specified.
;remote-random

# Keep trying indefinitely to resolve the
# host name of the OpenVPN server.  Very useful
# on machines which are not permanently connected
# to the internet such as laptops.
resolv-retry infinite

# Most clients don't need to bind to
# a specific local port number.
nobind

# Downgrade privileges after initialization (non-Windows only)
#user nobody
#group nobody

# Try to preserve some state across restarts.
persist-key
persist-tun

# If you are connecting through an
# HTTP proxy to reach the actual OpenVPN
# server, put the proxy server/IP and
# port number here.  See the man page
# if your proxy server requires
# authentication.
;http-proxy-retry # retry on connection failures
;http-proxy [proxy server] [proxy port #]

# Wireless networks often produce a lot
# of duplicate packets.  Set this flag
# to silence duplicate packet warnings.
mute-replay-warnings

# SSL/TLS parms.
# See the server config file for more
# description.  It's best to use
# a separate .crt/.key file pair
# for each client.  A single ca
# file can be used for all clients.
ca ca.crt
cert ios.crt
key ios.key

# Verify server certificate by checking
# that the certicate has the nsCertType
# field set to "server".  This is an
# important precaution to protect against
# a potential attack discussed here:
#  http://openvpn.net/howto.html#mitm
#
# To use this feature, you will need to generate
# your server certificates with the nsCertType
# field set to "server".  The build-key-server
# script in the easy-rsa folder will do this.
;ns-cert-type server

# If a tls-auth key is used on the server
# then every client must also have the key.
;tls-auth ta.key 1

# Select a cryptographic cipher.
# If the cipher option is used on the server
# then you must also specify it here.
# Note that v2.4 client/server will automatically
# negotiate AES-256-GCM in TLS mode.
# See also the ncp-cipher option in the manpage
cipher AES-256-CBC


# Enable compression on the VPN link.
# Don't enable this unless it is also
# enabled in the server config file.
;compress

# Set log file verbosity.
verb 3

# Silence repeating messages
;mute 20
</pre>

<p><br>Step 4: Plug iPhone into your Mac and follow the steps below to import 4 files into OpenVPN Connect: ca.crt, ios.crt, ios.key and ios.ovpn </p>

<pre>
Open iTunes
Select your device on the top
Go to the Apps tab
Scroll to the bottom file sharing section
Select the OpenVPN application
Add all mentioned files (ca.crt, ios.crt, ios.key and ios.ovpn) on the right hand side
</pre>

<p><br>Step 5: Launch OpenVPN Connect on your iPhone and add the profile by click the + button.</p>

<p><br>Step 6: Enjoy safer Internet on your iPhone!</p>



<p><br><br>Are you also looking for the instructions for the server? No worries. Check this out - <a href="https://github.com/fredmeng/OpenVPN-Server" target="_blank">Build your private OpenVPN server on Amazon AWS</a>. </p>
