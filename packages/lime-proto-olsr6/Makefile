#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

LIME_BUILDDATE:=$(shell date +%Y%m%d_%H%M)
LIME_CODENAME:=bigbang

GIT_COMMIT_DATE:=$(shell git log -n 1 --pretty=%ad --date=short . )
GIT_COMMIT_TSTAMP:=$(shell git log -n 1 --pretty=%at . )

PKG_NAME:=lime-proto-olsr6
PKG_VERSION=$(GIT_COMMIT_DATE)-$(GIT_COMMIT_TSTAMP)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	TITLE:=LiMe OLSR proto support (IPv6)
	CATEGORY:=LiMe
	MAINTAINER:=leonaard <leone@inventati.org>
	URL:=http://libre-mesh.org
	DEPENDS:=+lua +libuci-lua +lime-system +olsrd +olsrd-mod-jsoninfo
endef

define Build/Compile
	@rm -rf ./build || true
	@cp -r ./src ./build
	@sed -i '/^--!.*/d' build/*.lua
endef

define Package/$(PKG_NAME)/install
	@mkdir -p $(1)/usr/lib/lua/lime/proto || true
	$(CP) ./build/olsr6.lua $(1)/usr/lib/lua/lime/proto/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
