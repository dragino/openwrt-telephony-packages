#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=asterisk11-chan-sccp-b
PKG_REV:=5845
PKG_VERSION:=v4.2-r$(PKG_REV)
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://svn.code.sf.net/p/chan-sccp-b/code/tags/openwrt
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=svn

PKG_FIXUP:=autoreconf -fi

PKG_LICENSE:=GPL-1.0
PKG_LICENSE_FILES:=COPYRIGHT LICENSE
PKG_MAINTAINER:=Jiri Slachta <slachta@cesnet.cz>

include $(INCLUDE_DIR)/package.mk

define Package/asterisk11-chan-sccp-b
  SUBMENU:=Telephony
  SECTION:=net
  CATEGORY:=Network
  TITLE:=SCCP channel provider support
  URL:=http://chan-sccp-b.sourceforge.net/
  DEPENDS:=asterisk11 +libltdl
endef

define Package/asterisk11-chan-sccp-b/description
 SCCP channel provider for asterisk. It delivers extended functionality for SCCP phones over chan_skinny delivered
 by asterisk by default.
endef

define Build/Configure
	$(call Build/Configure/Default,--with-asterisk=$(STAGING_DIR)/usr/include/asterisk-11)
endef

define Build/Compile
	$(MAKE) -C "$(PKG_BUILD_DIR)" \
		CFLAGS="$(CFLAGS) -I$(PKG_BUILD_DIR)/src -DLOW_MEMORY" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/asterisk11-chan-sccp-b/conffiles
/etc/asterisk/sccp.conf
endef

define Package/asterisk11-chan-sccp-b/install
	$(INSTALL_DIR) $(1)/etc/asterisk
	$(CP) ./files/sccp.openwrt.conf $(1)/etc/asterisk/sccp.conf
	$(INSTALL_DIR) $(1)/usr/lib/asterisk/modules
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/asterisk/modules/chan_sccp.so $(1)/usr/lib/asterisk/modules/
endef

$(eval $(call BuildPackage,asterisk11-chan-sccp-b))
