OpenWrt BOINC client feed
=========================

This repository supports the synchronisation of developments in support
of Volunteer Computing with BOINC on the OpenWrt platform: It brings
BOINC to small devices, i.e the edge of the internet.

No regular user is meant to work with this repository. I only holds packages
to support scientific apps on OpenWrt which are eventually distributed by
the respective BOINC project if not run as an anonymous platform.
The 'boinc' OpenWrt package itself is 
available via the official community packages at
https://github.com/openwrt/packages/tree/master/net/boinc.

To contribute, you need the OpenWRT SDK for your target platform and
preferably also for X86_64 to test quickly on an OpenWrt instance under
Virtualbox. This git repository o a local clone of it we suggest to
add as a custom feed to your SDK.
