include $(TOPDIR)/rules.mk

PKG_NAME:=hickory-dns
PKG_VERSION:=2025.06.27
PKG_RELEASE:=$(AUTORELEASE)

HICKORY_COMMIT:=00452fbac35a0ff1efd74fcf070454f75051588d

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/hickory-dns/hickory-dns/tar.gz/00452fbac35a0ff1efd74fcf070454f75051588d?
PKG_HASH:=3e52b936ce5feb096c24ec1c1debec4341eba37687b7f6867a80509574f38db3

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-00452fbac35a0ff1efd74fcf070454f75051588d

PKG_BUILD_DEPENDS:=rust/host
PKG_BUILD_PARALLEL:=1

RUST_PKG_FEATURES:=resolver,tls-ring,https-ring,quic-ring,h3-ring,rustls-platform-verifier,sqlite,prometheus-metrics

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/rust/rust-package.mk

define Package/hickory-dns
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=A plug-in DNS forwarder/splitter
  URL:=https://github.com/hickory-dns/hickory-dns
  DEPENDS:=$(RUST_ARCH_DEPENDS)
endef

define Build/Compile
  $(call Build/Compile/Cargo,bin,--no-default-features)
endef

define Package/hickory-dns/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/* $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/etc/hickory-dns/
	$(INSTALL_BIN) ./files/etc/init.d/hickory-dns $(1)/etc/init.d/hickory-dns
	$(INSTALL_BIN) ./files/etc/hickory-dns/forwarder.toml $(1)/etc/hickory-dns/forwarder.toml
	echo "$(HICKORY_COMMIT)" > $(1)/etc/hickory-dns/commit
endef

$(eval $(call RustBinPackage,hickory-dns))
$(eval $(call BuildPackage,hickory-dns))
