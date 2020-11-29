## Configure Reverse Proxy In cPanel

Setting up a reverse proxy or a regular CentOS server is quite straight forward, however when you have cPanel included in the equation, you need to be aware of a few things. That is why I've decided to write this short post here.

Here is what you need to do in order to get the reverse proxy working on a cPanel server:


## Prerequisites
1. cPanel Server
2. Apache Modules
    1. [mod_proxy] ___-- Required___
    1. [mod_proxy_http] ___-- Required___
    1. [mod_proxy_connect] ___-- Required___
    3. [mod_proxy_wstunnel] _-- Optional. enable if you want to use WebSockets_


## Lets Get Started

### Setup Apache Modules
#### Login to WHM and navigate To `Home » Software » EasyApache 4`

![Easy Apache Menu](https://s2.do-spaces.com/2020/Nov/29/160664814488.jpg)

#### Click `Customize` On **Currently Installed Packages**

![Customize Button](https://s2.do-spaces.com/2020/Nov/29/160664821549.jpg)

#### Once it loaded click `Apache Modules` In the Left-side Menu

![Apache Modules Menu](https://s2.do-spaces.com/2020/Nov/29/16066482864.jpg)


#### Select All `REQUIRED` Proxy Modules That Mentioned Above
![Modules](https://s2.do-spaces.com/2020/Nov/29/16066488073.jpg)

Once you have selected the modules click **Review** in the left menu.

And click **Provision** To install & Setup the apache modules.

---

### Creating A Reverse Proxy
Create a new file if not already exists in the below locations

***STD*** -- Runs Without SSL
```
/usr/local/apache/conf/userdata/ssl/2_4/{user}/yourdomain.com/proxy_pass.conf
```

***SSL*** -- Runs With SSL
```
/usr/local/apache/conf/userdata/std/2_4/{user}/yourdomain.com/proxy_pass.conf
```

> (change '{user}' with the actual cPanel username')

Enable custom VHost file by running the below cmd
```
/scripts/ensure_vhost_includes --user={user}
```

 After that you can then add the custom rules at the custom Vhost files which we created before.
 
Add below config to those VHosts file. which will forword all the requests for a domain to the given IP and also allows cPanel to handle SSL if it uses WEB ROOT to fetch SSL

```
###### DO NOT REMOVE BELOW LINE. IT USED TO AUTO RENEW SSL VIA CPANEL ######
ProxyPass "/.well-known"  !
###### DO NOT REMOVE ABOVE LINE. IT USED TO AUTO RENEW SSL VIA CPANEL ######

ProxyPass "/"  "http://10.0.3.2:80/"
ProxyPassReverse "/"  "http://10.0.3.2:80/"
```

Next step is to make sure that the written config is valid. run the below cmd
```
service httpd configtest
```

If you get '`Syntax OK`' then run the below cmds to rebuild apache config & restart the Apache service

```
/scripts/rebuildhttpdconf 

service httpd restart
```

This pretty much it. All of this is required because you would lose all of your changes if you add them directly to your main httpd conf file.


---

I have also create a simple script which can handle creation of reverse proxy config in cPanel 

%[https://github.com/varunsridharan/cpanel-apache-proxy]

---


[mod_proxy]: http://httpd.apache.org/docs/current/mod/mod_proxy.html
[mod_proxy_http]: https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html
[mod_proxy_connect]: https://httpd.apache.org/docs/2.4/mod/mod_proxy_connect.html
[mod_proxy_wstunnel]: https://httpd.apache.org/docs/2.4/mod/mod_proxy_wstunnel.html

%%[blog-footer]