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
Virtualbox. This git repository or a local clone of it we suggest to
add as a custom feed to your SDK.


boinc-app-tngrid
----------------

This package provices the scientific app for [TN-GRID](http://gene.disi.unitn.it/test/).
OpenWrt platforms the project already supports can be inspected [here](https://gene.disi.unitn.it/test/apps.php)

The package was successfully tested on 
 * x86_64
 
Please create an issue to request packages for additional OpenWrt platforms.
The binary created by this packages cannot be distributed by the project
until a
[patch](https://github.com/VolunteerComputingHelp/openWRT-boinc-client/tree/master/boinc-app-tngrid)
providing a static library for bzip2 is accepted by OpenWrt.
