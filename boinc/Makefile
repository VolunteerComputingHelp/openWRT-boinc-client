# Copyright 2020 by Christian Dreihsig and Steffen Möller
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=boinc
PKG_VERSION:=7.16.5
PKG_VERSION_SHORT:=$(shell echo $(PKG_VERSION)| cut -f1,2 -d.)
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/BOINC/boinc
PKG_SOURCE_DATE:=2020-02-25
PKG_SOURCE_VERSION:=fbdcc2d6165f0a3897341852f0fcf91a934724d0
PKG_MIRROR_HASH:=f5ad881db7fafd6fc2c5360049d4f9c95c27d41641f5a77405d7df1514ecbc9f

PKG_MAINTAINER:=
PKG_CPE_ID:=cpe:/a:boinc_project:boinc

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/boinc/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=https://github.com/BOINC/boinc/
endef

define Package/boinc/Default/description
 The Berkeley Open Infrastructure for Network Computing (BOINC) is a
 software platform for distributed computing: several initiatives of
 various scientific disciplines all compete for the idle time of
 desktop computers. The developers' web site at the University of
 Berkeley serves as a common portal to the otherwise independently run
 projects.
endef

define Package/boinc
  $(call Package/boinc/Default)
  SUBMENU:=Computation
  TITLE:=BOINC client
  DEPENDS:=+curl +bzip2 +libstdcpp +libopenssl +zlib
  LICENSE:=GPL-3.0-or-later
  LICENSE_FILES:=COPYING
endef

define Package/boinc/description
$(call Package/boinc/Default/description)

 This package provides the BOINC core client program that is
 required to participate in any project that uses BOINC to control what
 projects to participate in and to determine constraint for the computation
 like the percentage of CPU time. OpenWRT does not
 provide the graphical BOINC Manager, but you can connect to this
 machine from the BOINC Manager of your desktop computer.
endef


CONFIGURE_ARGS += \
	--disable-server --disable-manager --enable-client --enable-libraries --disable-boinczip --enable-install-headers --enable-dynamic-client-linkage

define Build/InstallDev
	echo "*** BOINC *** InstallDev ***"
	$(INSTALL_DIR) $(1)/usr/include/boinc
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/boinc/* $(1)/usr/include/boinc/
	$(CP) $(PKG_BUILD_DIR)/*.h $(1)/usr/include/boinc/ # project_specific_defines.h, config.h, version.h, svn_version.h
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.a $(1)/usr/lib/
endef

define Package/boinc/install
	echo "*** BOINC *** install ***"
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.{la,so}* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/boinc-client $(1)/etc/init.d/boinc-client
	$(INSTALL_DIR) $(1)/opt/boinc
endef

$(eval $(call BuildPackage,boinc))
