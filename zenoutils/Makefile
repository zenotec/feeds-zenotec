
include $(TOPDIR)/rules.mk

PKG_NAME:=zenoutils
PKG_VERSION:=0.0.2
PKG_RELEASE=1


PKG_MAINTAINER:=Kevin Mahoney <kevin.mahoney@zenotec.net>
PKG_LICENSE:=CLOSED
PKG_LICENSE_FILES:=COPYING


PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:zenotec/common_zenoutils.git
PKG_SOURCE_VERSION:=68697166778a27760ea72bda1a4cd3649eb62f87
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DEPENDS:=boost libuuid

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/zenoutils
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Middleware
  TITLE:=Zeno Utilities
  DEPENDS:=+boost +libuuid +libpthread +librt $(CXX_DEPENDS)
  PROVIDES:=libzutils
  URL:=http://github.com/zenotec
endef

define Package/zenoutils/description
  Embedded software stack and utilities
endef

CONFIGURE_PATH = build
CONFIGURE_CMD = ../configure
MAKE_PATH = build

define Build/Configure
	( cd $(PKG_BUILD_DIR); ./autogen.sh )
	$(call Build/Configure/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) -a \
		$(PKG_INSTALL_DIR)/usr/include/zutils \
		$(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libzutils.{a,so*} \
		$(1)/usr/lib/
endef

define Package/zenoutils/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libzutils.{a,so*} \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,zenoutils))
