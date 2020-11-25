## Configure Pi-Hole With DNS over TLS - [ Private DNS ]

When Google officially launched [Android 9 Pie](https://www.android.com/versions/pie-9-0/), which includes a slew of new features around digital well-being, security, and privacy. 
If you’ve poked around the network settings on your phone, you may have noticed a new settings called **Private DNS Mode**.

## What is Private DNS?

The actual terminology for Private DNS is either DNS over TLS or DNS over HTTPS. TLS stands for Transport Layer Security and HTTPS stands for Hypertext Transfer Protocol Secure. 

> You can read more about [DNS over TLS / DNS over HTTPS](https://www.cloudflare.com/learning/dns/dns-over-tls/) at [cloudflare](https://www.cloudflare.com/learning/dns/dns-over-tls/)


## What is the need to use Pi-Hole With DNS over TLS ?
Well based on my experience not all adds are getting blocked with using Pi-hole as a dns resolver for the hole network. and android some show catches the IP Address of the add's website when its not configured to run with Private DNS. 

And another reason is when i am using with ***Mobile Internet*** i see a lots of adds. when using ***Private DNS*** its gets reduced. 

> I never used Raspberry Pi  to run Pi-Hole in my local network. so i haven't tested the below cmd with Raspbian OS.


### Step 1
Install Nginx using the below cmd

```shell
sudo apt-get  install nginx
```

### Step 2
DNS over TLS requires SSL so we will be using [Let’s Encrypt]

First, add the repository:

```shell
sudo add-apt-repository ppa:certbot/certbot
```
since we are using `Nginx` we need to install `Certbot Nginx Addon`

```shell
sudo apt-get install -y certbot python3-certbot-nginx
```

### Step 3
we need to generate a ssl certificate using [Let’s Encrypt]

Make sure to replace
1. `<your-email>` with your email ID
2. `<your-domain>` with the domain / subdomain you choose to use

```shell
sudo certbot  certonly --webroot -w "/var/www/html/" --preferred-challenges http -m "<your-email>" -d "<your-domain>" -n --agree-tos --no-eff-email
```

### Step 4
Create a new directory named `streams` inside `/etc/nginx/` and create a file `dns-over-tls` inside of `streams` directory with the below content

make sure to replace `{dns_domain_name}` with the actual domain name you decided to use 

```shell
upstream dns-servers {
	server    127.0.0.1:53;
}
server {
  listen 853 ssl; # managed by Certbot
  ssl_certificate /etc/letsencrypt/live/{dns_domain_name}/fullchain.pem; # managed by Certbot
  ssl_certificate_key /etc/letsencrypt/live/{dns_domain_name}/privkey.pem; # managed by Certbot
  ssl_protocols        TLSv1.2 TLSv1.3;
  ssl_ciphers          HIGH:!aNULL:!MD5;
		
  ssl_handshake_timeout    10s;
  ssl_session_cache        shared:SSL:20m;
  ssl_session_timeout      4h;
  proxy_pass dns-servers;
}
```

### Step 5 
Edit `/etc/nginx/nginx.conf` and add the below lines which tells nginx to auto include config files inside of `streams` directory

```shell
stream {
	include /etc/nginx/streams/*;
}
```

### Step 6 
Remove all the other server config which are located inside of `/etc/nginx/sites-available/` AND `/etc/nginx/sites-enabled/`

```shell
sudo rm -rf /etc/nginx/sites-available/*
sudo rm -rf /etc/nginx/sites-enabled/*
sudo service nginx start
```


> Make sure to have **TCP PORT** `853` open 
> now you can use the domain name in your android mobile in private dns setting.

---

I have also made a quick setup script which you can find @

%[https://github.com/varunsridharan/pi-hole-android-private-dns]

> if you need help in setting it up. you can contact me via [Twitter @varunsridharan2](https://twitter.com/varunsridharan2) i will do my best. 


---

%%[blog-footer]


[Let’s Encrypt]: https://letsencrypt.org/
