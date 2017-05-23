#
# Copyright (C) 2014 - Zenotec LLC
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME := rtap
PKG_VER:=0
PKG_SUBVER:=10
PKG_VERSION := $(PKG_VER).$(PKG_SUBVER)
PKG_RELEASE := $(PKG_VERSION)

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=33410a7c31af77629994be32bfb41cdbcf2004c5
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/zenotec/rtap-ko.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtap
    SUBMENU:=Network Support
    TITLE:=Wireless Packet forwarder
    FILES:= \
        $(PKG_BUILD_DIR)/$(PKG_NAME).$(LINUX_KMOD_SUFFIX)
    URL:=$(PKG_SOURCE_URL)
    MAINTAINER:=Kevin Mahoney <kevin.mahoney@zenotec.net>
    DEPENDS:=$(PKG_BUILD_DEPENDS)
    AUTOLOAD:=$(call AutoLoad,30,rtap)
endef

define KernelPackage/rtap/description
  A linux kernel module that listens for wireless frames and forwards them to a listener.
endef

define Build/Compile
	$(MAKE) -C $(LINUX_DIR) \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		PATCHLEVEL="$(LINUX_VERSION)" \
		KERNDIR="$(LINUX_DIR)" \
		SUBDIRS="$(PKG_BUILD_DIR)" \
                modules
endef

define KernelPackage/rtap/conffiles
devices
listeners
filters
endef

define KernelPackage/rtap/preinst
#!/bin/sh
rmmod rtap
endef

define KernelPackage/rtap/postinst
#!/bin/sh
modprobe rtap
endef

define KernelPackage/rtap/install
	$(INSTALL_DIR) $(1)/etc/rtap
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/rtap.init $(1)/etc/init.d/rtap
	$(INSTALL_DIR) $(1)/lib/modules/$(LINUX_VERSION)
	$(CP) $(PKG_BUILD_DIR)/$(PKG_NAME).$(LINUX_KMOD_SUFFIX) $(1)/lib/modules/$(LINUX_VERSION)/
endef

$(eval $(call KernelPackage,rtap))
