### How to setup dnsmasq on mac
> Here dnsmasq masks .test domain to localhost

-   `brew install dnsmasq`
-   `mkdir -pv $(brew --prefix)/etc/`
-   `sudo bash -c 'echo "address=/.test/127.0.0.1" >> /opt/homebrew/etc/dnsmasq.conf'` // send `.test` to localhost
-   `sudo brew services start dnsmasq`
-   `sudo mkdir -v /etc/resolver`
-   `sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/test'` // set nameserver for test -> locahost
-   `sudo brew services restart dnsmasq` // so that it runs on login