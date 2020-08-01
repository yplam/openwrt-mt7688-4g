include $(TOPDIR)/rules.mk

PKG_NAME:=mt7688-4g
PKG_VERSION:=mt7688-4g-1.0
PKG_BUILD_DIR:= $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=MT7688 4G router config scripts
	SUBMENU:=mt7688-4g
	DEPENDS:= +kmod-mt76 +luci +luci-proto-qmi +mwan3 +luci-app-mwan3

endef
# +luci-app-mwan3 
define Build/Compile
	true
endef

define Package/$(PKG_NAME)/install
	$(CP) -f ./files/* $(1)
endef


$(eval $(call BuildPackage,$(PKG_NAME)))