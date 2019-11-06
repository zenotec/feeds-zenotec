
include $(TOPDIR)/rules.mk

PKG_NAME:=wcap
PKG_VERSION:=1.0.0
PKG_RELEASE=1


PKG_MAINTAINER:=Kevin Mahoney <kevin.mahoney@zenotec.net>
PKG_LICENSE:=CLOSED
PKG_LICENSE_FILES:=COPYING


PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:zenotec/wcap.git
PKG_SOURCE_VERSION:=a7ee2ef1e803c445d802f3ed907af605de7e8850
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DEPENDS:=libnl

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/wcap
  SECTION:=network
  CATEGORY:=Utilities
  TITLE:=Wireless packet capture and forwarder
  DEPENDS:=+libnl-core +libnl-genl +libnl-route
  URL:=http://github.com/zenotec
endef

define Package/wcap/description
  Wireless frame capturer and forwarder
endef

CONFIGURE_PATH = build
CONFIGURE_CMD = ../configure
MAKE_PATH = build

define Build/Configure
	( cd $(PKG_BUILD_DIR); ./autogen.sh )
	$(call Build/Configure/Default)
endef

define Package/wcap/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/wcap $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,wcap))
