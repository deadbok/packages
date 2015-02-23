#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=git
PKG_VERSION:=2.3.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/software/scm/git/
PKG_MD5SUM:=e5880760d1f43f4f49b3bf94b9046eee

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/git
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Version Control Systems
  DEPENDS:=+libopenssl +libpthread +librt +GIT_curl:libcurl +@GIT_curl:LIBCURL_IMAP
  TITLE:=The fast version control system
  URL:=http://git-scm.com
  MAINTAINER:=Peter Wagner <tripolar@gmx.at>
  MENU:=1
endef

define Package/git/config
	source "$(SOURCE)/Config.in"
endef

define Package/git/description
 Git is a free & open source, distributed version control system
 designed to handle everything from small to very large projects
 with speed and efficiency.
endef

MAKE_FLAGS := \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	CPPFLAGS="$(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	NO_EXPAT="YesPlease" \
	NO_MKSTEMPS="YesPlease" \
	NO_GETTEXT="YesPlease" \
	NO_UNIX_SOCKETS="YesPlease" \
	NO_IPV6="YesPlease" \
	NO_ICONV="YesPlease" \
	NO_NSEC="YesPlease" \
	NO_PERL="YesPlease" \
	NO_PYTHON="YesPlease" \
	NO_TCLTK="YesPlease" \
	CURLDIR="$(STAGING_DIR)/usr"

ifeq ($(CONFIG_GIT_curl),)
MAKE_FLAGS+=NO_CURL="YesPlease"
endif

define Build/Configure
	@echo $(DEPENDS)
	@echo $(MAKE_FLAGS)   
	$(MAKE) -C $(PKG_BUILD_DIR) \
		configure

	( cd $(PKG_BUILD_DIR); \
		./configure --prefix=/usr \
	);
endef

define Package/git/install
	$(INSTALL_DIR) $(1)
	$(RM) $(PKG_INSTALL_DIR)/usr/bin/git-cvsserver
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

$(eval $(call BuildPackage,git))
