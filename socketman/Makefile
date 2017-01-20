# Copyright (C) 2016 Cucumber WiFi
#
# This is free software, licensed under the GNU General Public License v2.

export CT_ARCH="-D__OPENWRT__"
export CT_VERSION=0d94378

include $(TOPDIR)/rules.mk

PKG_NAME:=SocketMan
PKG_MAINTAINER:=Andrew Margarit <andrew@cucumberwifi.io>
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=0d94378beb0b2b36c81ef3ceb5cb142f0d389383
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE_URL:=https://github.com/cucumber-tony/SocketMan.git
PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_VERSION:=$(CT_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/socketman
SECTION:=net
CATEGORY:=Network
DEPENDS:=+libjson-c +curl +libcurl +libopenssl +libpthread +libmosquitto +@LIBCURL_OPENSSL +libc +libnl
TITLE:=SocketMan communication package for Cucumber Tony
URL:=http://www.cucumberwifi.io
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	mkdir -p $(PKG_BUILD_DIR)/build
	mkdir -p $(PKG_BUILD_DIR)/obj
	tar -C $(DL_DIR) -xzvf $(DL_DIR)/$(PKG_NAME).tar.gz
	$(CP) $(DL_DIR)/$(PKG_NAME)/src/* $(PKG_BUILD_DIR)/
endef

define Package/socketman/description
 This package contains the communication daemon for Cucumber Tony
endef

define Package/socketman/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/socketman $(1)/usr/bin/socketman
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/socketman.init $(1)/etc/init.d/socketman
endef

$(eval $(call BuildPackage,socketman))

.PHONY: clean
clean:
	rm -rf $(DL_DIR)/$(PKG_NAME)*
