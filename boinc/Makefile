#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=boinc
PKG_VERSION:=7.16.5
PKG_VERSION_SHORT:=$(shell echo $(PKG_VERSION)| cut -f1,2 -d.)
PKG_RELEASE:=1

#PKG_SOURCE_URL:=@GITHUB/boinc/client_release/$(PKG_VERSION_SHORT)/
PKG_SOURCE_URL:=https://github.com/BOINC/boinc/archive/client_release/$(shell echo $(PKG_VERSION))/
PKG_SOURCE:=$(PKG_VERSION).tar.gz
#MD5#PKG_HASH:=9a4a14cf2ef7ea9850d81ceac4adae9c
PKG_HASH:=33db60991b253e717c6124cce4750ae7729eaab4e54ec718b9e37f87012d668a

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

define Build/Prepare
	$(PKG_UNPACK)
	if [ -d $(PKG_BUILD_DIR)/boinc-$(PKG_VERSION) ]; then \
		echo "I: Moving source tree to: $(PKG_BUILD_DIR)" ; \
		mv boinc-client_release-$(PKG_VERSION_SHORT)-$(PKG_VERSION)/* $(PKG_BUILD_DIR)/ ; \
		rmdir boinc-client_release-$(PKG_VERSION_SHORT)-$(PKG_VERSION) ; \
	elif [ -d $(PKG_BUILD_DIR)/../boinc-$(PKG_VERSION) ]; then \
		echo "I: B Moving source tree to: $(PKG_BUILD_DIR)" ; \
		mv $(PKG_BUILD_DIR)/../boinc-client_release-7.16-7.16.5/* $(PKG_BUILD_DIR)/ ; \
		rm -rf ../boinc-client_release-$(PKG_VERSION_SHORT)-$(PKG_VERSION) ; \
	else \
		echo "E: Cannot find source tree" ; \
		echo "E: PKG_BUILD_DIR: $(PKG_BUILD_DIR)" ; \
		exit 1 ; \
	fi
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
	$(INSTALL_DIR) $(1)/etc
	$(CP) -r $(PKG_INSTALL_DIR)/etc/* $(1)/etc/
	$(INSTALL_DIR) $(1)/lib/systemd/system
	$(CP) $(PKG_INSTALL_DIR)/lib/systemd/system/* $(1)/lib/systemd/system
endef

$(eval $(call BuildPackage,boinc))
