# mail
Self-Hosted Email (Theoretical Preview)

Reference: https://mailinabox.email/guide.html

# Mail Domain

```
makari.io
```

A domain name that I own is **makari.io**.

".io" is the part of the domain known as the Top Level Domain (TLD), such as ".com", ".gov", etc.

```
AWS Route 53 > Domains > Registered Domains > Register Domains
```

My email user could have an address such as **jackson@makari.io**

# Mail Server
```
box.makari.io
```

This is the mail server's hostname. 

```
AWS Route 53 > Hosted Zones > Create Hosted Zone
```

A DNS "A Record" (named "box.makari.io") points to an AWS Elastic IP (a fixed IPv4 associated in AWS EC2 Console) of an AWS EC2 instance (a virtual server).

# Virtual Server

Setup AWS EC2 Instance (At least t2.micro but only Ubuntu 22.04 x64).

```
$ ssh -i "my-key-pair.pem" ec2-user@box.makari.io
$ sudo su
$ apt update && apt upgrade -y
$ reboot
$ ssh -i "my-key-pair.pem" ec2-user@box.makari.io
```

# Name Servers

Setup Glue Records in AWS Route 53 Registered Domains

```
ns1.box.makari.io # Elastic IP (IPv4)
ns2.box.makari.io # Elastic IP (IPv4)
```

# Reverse DNS

```
box.makari.io
```

# Hostname

```
$ ssh -i "my-key-pair.pem" ec2-user@box.makari.io
$ sudo su
$ vi /etc/hostname # box.makari.io
$ vi /etc/hosts
```

# Server User

```
$ ssh -i "my-key-pair.pem" ec2-user@box.makari.io
$ sudo su
$ adduser jackson
$ usermod -aG sudo jackson
$ cp -r ~/.ssh /home/jackson
$ chown jackson:jackson /home/jackson
$ exit
$ ssh -i "my-key-pair.pem" jackson@box.makari.io
```

# Install

```
$ ssh -i "my-key-pair.pem" jackson@box.makari.io
$ curl -s https://mailinabox.email/setup.sh | sudo -E bash # OK; jackson@makario.io; US; Pacific Ocean
$ sudo mailinabox # If Restart Needed
```
   
# Admin Portal

```
https://box.makari.io/admin
```

# Status Checks

Review recommendations.

# TLS (SSL) Certificates

```
Provision
```

# Email Inbox

```
https://box.makari.io/mail
```

# DNSSEC

```
AWS Route 53 > Hosted Zones > makari.io > DNSSEC signing
```

# Checking and Sending Mail

| Option | Value |
| --- | --- |
| Protocol/Method	| IMAP |
| Mail server	| box.makari.io |
| IMAP | Port	993 |
| IMAP Security	| SSL or TLS |
| SMTP Port	| 465 |
| SMTP Security	| SSL or TLS |
| Username:	| Your whole email address. |
| Password:	| Your mail password. |

