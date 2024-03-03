# This software is in the public domain, furnished "as is", without technical
# support, and with no warranty, express or implied, as to its usefulness for
# any purpose.

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=optoe
PKG_RELEASE:=0.1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ghhccghk/optoe-linux-device.git
PKG_SOURCE_VERSION:=d627514c64f0ecb0bb7890cd3c3db8b9a9c7cc32
PKG_MIRROR_HASH:=skip

PKG_MAINTAINER:=Don Bollinger (don@thebollingers.org)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/optoe
  SUBMENU:=I2C Support
  TITLE:=optoe kernel module
  FILES:=$(PKG_BUILD_DIR)/optoe.ko
  AUTOLOAD:=$(call AutoProbe,optoe)
endef

define KernelPackage/optoe/description
  Optoe is an i2c based driver that supports read/write access to all
  the pages (tables) of MSA standard SFP and similar devices (conforming
  to the SFF-8472 spec), MSA standard QSFP and similar devices (conforming
  to the SFF-8436 or SFF-8636 spec) and CMIS devices (conforming to the
  Common Management Interface Specification).
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	M="$(PKG_BUILD_DIR)"

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		CONFIG_PACKAGE_kmod-optoe=m \
		modules
endef

$(eval $(call KernelPackage,optoe))

