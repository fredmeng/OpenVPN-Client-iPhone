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
dev tun

# The hostname/IP and port of the server.
# You can have multiple remote entries
# to load balance between the servers.
remote ec2-1-2-3-4.x.compute.amazonaws.com 1194 udp

# Keep trying indefinitely to resolve the
# host name of the OpenVPN server.  Very useful
# on machines which are not permanently connected
# to the internet such as laptops.
resolv-retry infinite

# Most clients don't need to bind to
# a specific local port number.
nobind

# Try to preserve some state across restarts.
persist-key
persist-tun

# SSL/TLS parms.
# See the server config file for more
# description.  It's best to use
# a separate .crt/.key file pair
# for each client.  A single ca
# file can be used for all clients.
ca ca.crt
cert iphone.crt
key iphone.key

# Enable compression on the VPN link.
# Don't enable this unless it is also
# enabled in the server config file.
;comp-lzo

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
