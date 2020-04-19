#
# Copyright (C) 2020 Steffen Moeller <moeller@debian.org>
#                    Christian Dreihsig
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=boinc-app-tngrid
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://bitbucket.org/francesco-asnicar/pc-boinc/get/
PKG_SOURCE:=2289f23f676f.zip
#MD5#PKG_HASH:=9a4a14cf2ef7ea9850d81ceac4adae9c
PKG_HASH:=b1345b821e6593c95b8a1da00954ce898e3de0e6856a355da35fadbbb20a1331

PKG_MAINTAINER:=Steffen Moeller <moeller@debian.org>
PKG_CPE_ID:=cpe:/a:boinc_project:tngrid

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

define Package/boinc-app-tngrid
  SECTION:=net
  CATEGORY:=Network
  URL:=https://bitbucket.org/francesco-asnicar/pc-boinc.git
  SUBMENU:=Computation
  TITLE:=TN-GRID app
  DEPENDS:=+boinc +libcares
  LICENSE:=GPL-3.0-or-later
  LICENSE_FILES:=Readme.md
endef

define Package/boinc-app-tngrid/description
  This package is only or internal use. It provides the binary for the TN-GRID BOINC project.
endef

define Build/Prepare
	$(PKG_UNPACK)
	mv $(PKG_BUILD_DIR)/../francesco-*-pc-boinc-*/* $(PKG_BUILD_DIR)/
	rm -rf $(PKG_BUILD_DIR)/../francesco-*-pc-boinc-*/
	echo "*** TN-GRID *** PATCHING ***"
	$(Build/Patch)
endef

#LDLIBBZ2="$(wildcard $(TOPDIR)/staging_dir/target-*/usr/lib/)/libbz2.a";
LDLIBBZ2="-lbz2"
BOINC_API_DIR=$(wildcard $(TOPDIR)/staging_dir/target-*/usr/include/boinc/ )
define Build/Compile
	# executing from /home/me/openwrt/sdk/build_dir/target-arm_cortex-a9+vfpv3_musl_eabi/boinc-app-tngrid-0.0.1/src
	echo "*** TN-GRID *** BUILDING ($(shell pwd)) ***"
	echo "*** TN-GRID *** TOPDIR ($(TOPDIR)) ***"
	cd $(PKG_BUILD_DIR) \
	   && cd src \
	   && $(MAKE) \
                      AR="$(TARGET_AR)" \
                      AS="$(TARGET_CC) -c $(TARGET_ASFLAGS)" \
                      LD=$(TARGET_CROSS)ld \
                      NM="$(TARGET_NM)" \
                      CC="$(TARGET_CC)" \
                      GCC="$(TARGET_CC)" \
                      CXX="$(TARGET_CXX)" \
                      RANLIB="$(TARGET_RANLIB)" \
                      STRIP=$(TARGET_CROSS)strip \
	              LDFLAGS=$(LDFLAGS) \
	  	      CPPFLAGS="$(CPPFLAGS) -I$(BOINC_API_DIR) -I. -Isimd" \
	  	      LDLIBBZ2="$(LDLIBBZ2)" \
	              BOINC_DIR="$(wildcard $(TOPDIR)/staging_dir/target-*/usr/include/boinc/ )" \
	              BOINC_API_DIR="$(BOINC_API_DIR)" \
	              BOINC_LIB_DIR="$(wildcard $(TOPDIR)/staging_dir/target-*/usr/lib/ )"
endef

define Build/Install
	cd $(PKG_BUILD_DIR) \
	   && cd src \
	   && $(MAKE) DESTDIR="$(PKG_INSTALL_DIR)" install
endef

define Build/InstallDev
	echo "*** TN-GRID InstallDev ($(shell pwd)) ***"
endef

define Package/boinc-app-tngrid/install
	echo "*** TN-GRID install ($(shell pwd)) ***"
	$(CP) -r $(PKG_INSTALL_DIR)/usr $(1)
endef

$(eval $(call BuildPackage,boinc-app-tngrid))
