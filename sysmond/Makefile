
include $(TOPDIR)/rules.mk

PKG_NAME:=sysmon
PKG_VERSION:=0.0.3
PKG_RELEASE=1


PKG_MAINTAINER:=Kevin Mahoney <kevin.mahoney@zenotec.net>
PKG_LICENSE:=CLOSED
PKG_LICENSE_FILES:=COPYING


PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:zenotec/zenoponics_sysmond.git
PKG_SOURCE_VERSION:=7b17061c6f5f191680b1503e8f0e9f63dd3af0d4
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DEPENDS:=zenoutils

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/sysmon
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=System Monitor
  DEPENDS:=+zenoutils
  URL:=http://github.com/zenotec
endef

define Package/sysmon/description
  Zenoponics System monitor
endef

CONFIGURE_PATH = build
CONFIGURE_CMD = ../configure
MAKE_PATH = build

define Build/Configure
	( cd $(PKG_BUILD_DIR); ./autogen.sh )
	$(call Build/Configure/Default)
endef

define Package/sysmon/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/sysmond.init $(1)/etc/init.d/sysmond
	$(CP) \
		./files/sysmond.conf \
		$(1)/etc/sysmond.conf
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/sysmond \
		$(PKG_INSTALL_DIR)/usr/bin/sysmon_cli \
		$(1)/usr/bin/
endef

$(eval $(call BuildPackage,sysmon))
