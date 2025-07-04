include $(TOPDIR)/rules.mk

PKG_NAME:=hickory-dns
PKG_VERSION:=2025.07.03
PKG_RELEASE:=$(AUTORELEASE)

HICKORY_COMMIT:=9c733c63a440f525eea2b44564ec3f806479d0df

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/hickory-dns/hickory-dns/tar.gz/9c733c63a440f525eea2b44564ec3f806479d0df?
PKG_HASH:=a45395a074ce4862ab235e0088c2a92857d790605d030d19d9de4990138d5ffc

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-9c733c63a440f525eea2b44564ec3f806479d0df

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
