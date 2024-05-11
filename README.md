# one-solution
A program for keeping one.com A DNS records up to date at one.com

## Required Packages
* [Python 3](https://www.python.org/) (Tested with Python 3.11.2)
* [curl](https://curl.se/) for ip resolution.

## Usage

```shell
$ python3 one-solution --config config.ini
```

## Example config.ini file

```ini
[DEFAULT]
# Default values are inherited by all other sections.

# Your one.com credentials
username = billy@mail.com
password = abcd1234

# Default ip to set all domains to. Incase it's unset the program will use the 
# ip resolver instead. 
# The config value will then overload the empty ip value back into the 
# configuration map and be inherited by all other sections.
ip = 

# A script to run. Must return a ip address with no other characters.
# Can be as simple as `cat ip.txt`.
ip_resolver = curl 'https://api.ipify.org'
# An alternative script. 
#ip_resolver = dig +short myip.opendns.com @resolver1.opendns.com

# Default path for where the last ip should be stored inbetween program 
# executions.
# If the last_ip_file is set and contains a value equal to the current ip 
# address the last_ip_file will cease to update the domain as the ip has not 
# been changed. 
# If the ip differs or no last_ip_file existed the last_ip_file will
# be (re)created with the new ip address.
# The last_ip_folder is not necessary if last_ip_file is written as a full path.
last_ip_folder = /tmp/one-solution/
last_ip_file = last-ip.txt

# How long the ip should be held valid for when looked up.
ttl = 3600

# Example domain to keep updated. Must not contain a subdomain.
# i.e 'example1.com' not 'www.example1.com'
[example1.com]
# List of subdomains you want pointing to your ip, 
# sepparated by ','.
subdomains = myddns,docs,www

# To have the head domain itself be kept updated set to True here.
update_domain = True

# Another domain to keep updated
[example2.com]
update_domain = False

[example3.com]
...
```

# Caveats
Note that the program is not capable of creating new DNS records.
It can only edit existing ones.

## Contributing
Pull requests are welcome. 
For major changes, please open an issue first to discuss what you would like to 
change.

Any feature requests are welcome as well.

## Need Help?
Don't hesitate to contact me: nils.edvin.eriksson@gmail.com

## Credit
Credit is due to [Luca](https://github.com/lgc-4) 
and his original work on [one.com-ddns-python-script](https://github.com/lgc-4/one.com-ddns-python-script)
where this projekt is forked from.
