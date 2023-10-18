include $(TOPDIR)/rules.mk

PKG_NAME:=hickory-dns
PKG_VERSION:=bb20324
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/hickory-dns/hickory-dns/tar.gz/$(PKG_VERSION)?
PKG_HASH:=94f0a41cebe0f9093f1a1183195b949ea1d84e8f26133d5bc73251adba4f61ee

PKG_BUILD_DEPENDS:=rust/host
PKG_BUILD_PARALLEL:=1

RUST_PKG_FEATURES:=dns-over-https-rustls,dns-over-quic,dns-over-h3,recursor,webpki-roots

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/rust/rust-package.mk

define Package/hickory-dns
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=A plug-in DNS forwarder/splitter
  URL:=https://github.com/hickory-dns/hickory-dns
  DEPENDS:=$(RUST_ARCH_DEPENDS) +ca-bundle
endef

define Build/Compile
  $(call Build/Compile/Cargo,bin)
endef

$(eval $(call RustBinPackage,hickory-dns))
$(eval $(call BuildPackage,hickory-dns))
