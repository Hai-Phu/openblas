include $(TOPDIR)/rules.mk

PKG_NAME:=OpenBLAS
PKG_VERSION:=0.3.9
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/OpenBLAS-$(PKG_VERSION)
PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/xianyi/OpenBLAS/archive/
PKG_HASH:=28cc19a6acbf636f5aab5f10b9a0dfe1
include $(INCLUDE_DIR)/package.mk

define Package/openblas
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=An optimized BLAS library
  URL:=https://www.openblas.net/
endef

define Package/bridge/description
  OpenBLAS is an optimized BLAS library based on GotoBLAS2 1.13 BSD version
endef
# Package build instructions; invoke the GNU make tool to build our package
define Build/Compile
        $(MAKE) -C $(PKG_BUILD_DIR) \
           NOFORTRAN=1 \
           TARGET='' \
           HOSTCC=gcc \
               CC="$(TARGET_CC)" \
           CFLAGS="$(TARGET_CFLAGS)" \
          LDFLAGS="$(TARGET_LDFLAGS)" 
endef
define Build/InstallDev
        $(INSTALL_DIR) $(1)/usr/lib/pkgconfig
        $(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
        $(INSTALL_DIR) $(1)/usr/include
        $(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
        $(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
endef

define Package/openblas/install
        $(INSTALL_DIR) $(1)/usr/lib
        $(CP) $(INSTALL_BIN) $(PKG_BUILD_DIR)/usr/lib/libOpenblas.so* $(1)/usr/lib/
endef
$(eval $(call BuildPackage,openblas))