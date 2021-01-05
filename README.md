Set up your own SIP address, place Audio/Video/SMS calls as sending mail via email address.
e.g. sip:1001@sip.domain.org

#Install and clean up default config files.
1. apt install asterisk asterisk-opus  (asterisk-opus is optional to enable opus codes)
2. mv /etc/asterisk /etc/asterisk.sample #Do NOT use the default configs.
3. cd /etc
4. git clone https://github.com/basncy/my-sip-address.git asterisk
5. chown -R asterisk:asterisk asterik #keep the owner same as default.
6. systemctl restart asterisk

#Minimal settings
1. on router, do port mapping.
	udp 6060 defined in pjsip.conf
	tcp 6060 defined in pjsip.conf
	udp 8000-9000 defined in rtp.conf
2. edit pjsip.conf
	put your LAN into localnet
	put your public ip address or domain name into external_signaling_address

#(Option) Advanced settings.
1. Keep your DDNS A recored updated.
2. Add SRV DNS record if listen on none standard port: _sip._udp.sip.ddns.org 0 0 6060 sip.ddns.org
3. Add SRV DNS record if listen on none standard port: _sip._tcp.sip.ddns.org 0 0 6060 sip.ddns.org

#Client.
1. linphone is open source with full features, download from linphone.org

#DEBUG
asterisk -rvvvv
pjsip set logger host 192.168.0.1
rtp set debug on
