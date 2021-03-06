#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=grilo-plugins
PKG_VERSION:=0.3.10
PKG_RELEASE:=1

PKG_MAINTAINER:=W. Michael Petullo <mike@flyn.org>
PKG_LICENSE:=LGPLv2.1
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/grilo-plugins/0.3/
PKG_HASH:=803b360fdb6d5fde1e647bdc40c16de3031b1a95b347b48b65fe4fc27a548d4a

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=meson/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../../devel/meson/meson.mk

define Package/grilo-plugins/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=grilo-plugins
  URL:=https://wiki.gnome.org/Projects/Grilo
endef

define Package/grilo-plugins
  $(call Package/grilo-plugins/Default)
  MENU:=1
  DEPENDS:=+grilo $(ICONV_DEPENDS) $(INTL_DEPENDS)
  TITLE:=Plugins for the Grilo framework
endef

define Package/grilo/decription
  Grilo is a framework that provides access to different sources of
  multimedia content, using a pluggable system. This package contains
  plugins to get information from a number of sources.
endef

MESON_ARGS += \
	-Denable-filesystem=no \
	-Denable-optical-media=no \
	-Denable-youtube=no \
	-Denable-flickr=no \
	-Denable-podcasts=no \
	-Denable-bookmarks=no \
	-Denable-lua-factory=no \
	-Denable-metadata-store=no \
	-Denable-vimeo=no \
	-Denable-tracker=no \
	-Denable-local-metadata=no \
	-Denable-chromaprint=no \
	-Denable-thetvdb=no \
	-Denable-tmdb=no \
	-Denable-freebox=no \

define Package/grilo-plugins/install
	$(INSTALL_DIR) $(1)/usr/lib/grilo-0.3
endef

define BuildPlugin
  define Package/grilo-plugins-$(1)
    $(call Package/grilo-plugins/Default)
    DEPENDS:=grilo-plugins
    ifneq ($(4),)
      DEPENDS+= $(4)
    endif
    TITLE:=$(2) plugin
  endef

  define Package/grilo-plugins-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/grilo-0.3
	for p in $(3); do \
		$(CP) $(PKG_INSTALL_DIR)/usr/lib/grilo-0.3/libgrl$$$$$$$${p}.so $$(1)/usr/lib/grilo-0.3; \
	done
  endef

  $$(eval $$(call BuildPackage,grilo-plugins-$(1)))
endef

$(eval $(call BuildPackage,grilo-plugins))

$(eval $(call BuildPlugin,dleyna,DLNA sharing,dleyna,,30))
# This is currently disabled because it won't work with libdmapsharing-4.0.so
#$(eval $(call BuildPlugin,dmap,DAAP and DPAP sharing,daap dpap,libdmapsharing,30))
$(eval $(call BuildPlugin,gravatar,Gravatar provider,gravatar,,30))
$(eval $(call BuildPlugin,jamendo,Jamendo sharing,jamendo,,30))
$(eval $(call BuildPlugin,magnatune,Magnatune sharing,magnatune,,30))
$(eval $(call BuildPlugin,opensubtitles,Open subtitles provider,opensubtitles,,30))
$(eval $(call BuildPlugin,raitv,Rai.tv sharing,raitv,,30))
$(eval $(call BuildPlugin,shoutcast,SHOUTcast sharing,shoutcast,,30))
