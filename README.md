# vpn-fix

![demo](http://recordit.co/7PSGvdZTkT)

Do you use a (**insert favourite curse word here**) corporate VPN? Does it route all of your traffic and slow your life down?

This tool will fix that problem in less than five minutes...

Only tested on OSX but it might work on linux if you're lucky.

## Setup (OSX)

clone this repo down:

```
$ git clone https://github.com/darahayes/vpn-fix
```

### Whitelist

Copy `whitelist.sample.txt` to `whitelist.txt` and add in IP addresses and/or hosts you want to access through the VPN **One per each line**.

e.g.

```
nearform.com
github.com
1.2.3.4
5.6.7.8
```

### Set the iface variable

 For most OSX users your active network interface is `en0`.

Double check by running `ifconfig` and finding which interface actually connects you to the internet.
If it's not `en0` then modify line 5 of `vpn-fix` and set the `iface` variable to your actual interface.

### Setup Script

The `setup` script creates an alias command in your `~/.profile` that runs the `vpn-fix` script, passing in the whitelist.

```
$ ./setup
alias created. Run source ~/.profile and then run vpnfix
```

### Run

Now whenever you connect to the VPN you can run `vpnfix`. It will prompt for your password.

```
dara@Daras-MacBook-Pro vpn-fixer $ vpnfix
Removing Fortinet's route all the things rule
delete net default: gateway ppp0
Now route all the things through normal connection!
add net default: gateway en0
Now route only things in your whitelist through VPN
Adding IP addresses for nearform.com to whitelist
Adding IP addresses for github.com to whitelist
Adding 1.2.3.4 to whitelist
Adding 5.6.7.8 to whitelist
add host 54.247.160.180: gateway ppp0
add host 192.30.253.113: gateway ppp0
add host 192.30.253.112: gateway ppp0
add host 1.2.3.4: gateway ppp0
add host 5.6.7.8: gateway ppp0
```

You can also easily update your whitelist and and run again.
