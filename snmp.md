### SNMP
`sudo apt-get install snmpd snmp`  
`sudo apt-get install snmp-mibs-downloader `     
`sudo download-mibs`  
`systemctl restart snmpd`  
`snmpget 127.0.0.1 -v 2c -c public .1.3.6.1.2.1.1.3.0`
