#
# KMP Hack!!!
#  	https://github.com/Entware/entware-ng-oldpackages-ports/blob/master/rsnapshot/Makefile
#	https://gitlab.nic.cz/turris/openwrt-packages/commit/98989f0e37ebf26f340975372ba2c7522bb79a20#177e86e2db96d388793eddf93c74f32598006022

include $(TOPDIR)/rules.mk

PKG_NAME:=rsnapshot
PKG_VERSION:=1.4.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/rsnapshot/rsnapshot/releases/download/$(PKG_VERSION)
PKG_MD5SUM:=860382f19e38fc649f9447397b54e442

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/rsnapshot
  SUBMENU:=Backup
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=rsnapshot Backup
  URL:=http://www.rsnapshot.org/
  DEPENDS:=+rsync +perl \
		+perlbase-autoloader \
		+perlbase-class \
		+perlbase-cwd \
		+perlbase-dirhandle \
		+perlbase-essential \
		+perlbase-fcntl \
		+perlbase-file \
		+perlbase-getopt \
		+perlbase-io \
		+perlbase-ipc \
		+perlbase-posix \
		+perlbase-selectsaver \
		+perlbase-tie \
		+perlbase-xsloader
endef

define Package/rsnapshot/description
  rsnapshot is a filesystem snapshot utility for making backups of local and
  remote systems.

  Using rsync and hard links, it is possible to keep multiple, full backups
  instantly available. The disk space required is just a little more than the
  space of one full backup, plus incrementals.
endef

CONFIGURE_ARGS += \
	--without-logger

CONFIGURE_VARS += \
	ac_cv_path_PERL=/usr/bin/perl \
	ac_cv_path_RSYNC=/usr/bin/rsync \
	ac_cv_path_CP=/bin/cp \
	ac_cv_path_RM=/bin/rm \
	ac_cv_path_DU=/usr/bin/du \
	ac_cv_path_SSH=/usr/bin/ssh

define Build/Configure
	$(call Build/Configure/Default)
	touch $(PKG_BUILD_DIR)/rsnapshot.{1,html}
	touch $(PKG_BUILD_DIR)/rsnapshot-diff.1
endef

define Package/rsnapshot/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
	    $(PKG_INSTALL_DIR)/usr/bin/$(PKG_NAME){,-diff} \
	    $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) \
	    $(PKG_INSTALL_DIR)/etc/$(PKG_NAME).conf.default \
	    $(1)/etc/$(PKG_NAME).conf
endef

define Package/rsnapshot/conffiles
/etc/$(PKG_NAME).conf
endef

$(eval $(call BuildPackage,rsnapshot))