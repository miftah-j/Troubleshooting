
# Temporary failure resolving bd.archive.ubuntu.com

**Root cause (first principles):**  
`Temporary failure resolving 'bd.archive.ubuntu.com'` = **DNS failure**, not an APT problem.
APT can’t download because your system **cannot resolve domain names**. Running `apt-get update` won’t fix it unless the DNS/network is fixed first.

----------

## Step 1 — Check Network Connectivity

Run:

    ping  -c  4  8.8.8.8

**If this fails** → You have **no internet / gateway issue**.  
Check IP:

    ip a  
    ip route

You should see:

-   An IP address (not 169.254.x.x)
-   A default route like:
    

> default via 192.168.x.1

If missing:

    sudo dhclient

----------
## Step 2 — Fix DNS (Most likely issue)

Check DNS:

    cat /etc/resolv.conf

If empty or wrong, set public DNS:

    sudo nano /etc/resolv.conf

Add:

    nameserver 8.8.8.8  
    nameserver 1.1.1.1

Save, then test:

    ping  -c  4 google.com

If this works → DNS fixed.

----------

## Step 3 — If using systemd-resolved (Ubuntu default)

Check status:

    systemctl status systemd-resolved

If inactive:

    sudo systemctl restart systemd-resolved

Then:

    sudo  ln  -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

----------

## Step 4 — Now fix APT

After DNS works:

    sudo apt-get clean  
    sudo apt-get update  
    sudo apt-get install -f

----------

## Step 5 — If you’re inside VM (Common in labs)

Pressure-test environment:

**VirtualBox**

> -   Network → Adapter → NAT or Bridged
    
**VMware**

> -   Adapter → NAT

Then inside VM:

    sudo dhclient

----------

## Step 6 — Bangladesh mirror issue (strategic fix)

Sometimes `bd.archive.ubuntu.com` is unreliable.

Switch to main mirror:

    sudo nano /etc/apt/sources.list

Replace:

> bd.archive.ubuntu.com

with:

> archive.ubuntu.com

Then:

    sudo apt-get update

----------

## Quick Diagnostic Flow (Use this order)

1.  `ping 8.8.8.8` → Network?
    
2.  `ping google.com` → DNS?
    
3.  Fix `/etc/resolv.conf`
    
4.  Restart `systemd-resolved`
    
5.  Update APT
    

----------

## Strategic Insight (Admin mindset)

This error is **not package-related**.  
It’s a **Layer 3/4 resolution failure**.

When you see:

> Temporary failure resolving

Always think:

**Network → DNS → Mirror**

That’s the professional troubleshooting sequence.
