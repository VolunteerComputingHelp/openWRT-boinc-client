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
PKG_SOURCE:=5371d4dbff7b.tar.gz
#MD5#PKG_HASH:=9a4a14cf2ef7ea9850d81ceac4adae9c
PKG_HASH:=11d3aec2f4049a08d817dec29574d95774468ec5b8487c9d5468bba3a0ca37cd

PKG_MAINTAINER:=Steffen Moeller <moeller@debian.org>
PKG_CPE_ID:=cpe:/a:boinc_project:tngrid

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

define Package/boinc-app-tngrid/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=https://bitbucket.org/francesco-asnicar/pc-boinc.git
endef

define Package/boinc-app-tngrid/Default/description
  This package is only or internal use. It provides the binary for the TN-GRID BOINC project.
endef

define Package/boinc-app-tngrid
  $(call Package/boinc-app-tngrid/Default)
  SUBMENU:=Computation
  TITLE:=TN-GRID app
  DEPENDS:=+boinc +c-ares
  LICENSE:=GPL-3.0-or-later
  LICENSE_FILES:=Readme.md
endef

define Package/boinc-app-tngrid/description
$(call Package/boinc-app-tngrid/Default/description)
endef

define Build/Prepare
	$(PKG_UNPACK)
	mv $(PKG_BUILD_DIR)/../francesco-*-pc-boinc-*/* $(PKG_BUILD_DIR)/
	rm -rf $(PKG_BUILD_DIR)/../francesco-*-pc-boinc-*/
	echo "*** TN-GRID *** PATCHING ***"
	$(Build/Patch)
endef

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
	  	      CPPFLAGS="$(CPPFLAGS) -I. -I../boinc_stub/api -Isimd" \
	              BOINC_DIR="$(wildcard $(TOPDIR)/staging_dir/target-*/usr/include/boinc/ )" \
	              BOINC_API_DIR="$(wildcard $(TOPDIR)/staging_dir/target-*/usr/include/boinc/ )" \
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
