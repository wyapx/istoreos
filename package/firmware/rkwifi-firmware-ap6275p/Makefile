# SPDX-License-Identifier: GPL-2.0-or-later

include $(TOPDIR)/rules.mk

PKG_NAME:=rkwifi-firmware-ap6275p
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ophub/firmware
PKG_SOURCE_VERSION:=3434f0ba9abcc29860858a36bd44a2736197ff76
PKG_MIRROR_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define Package/rkwifi-firmware-ap6275p
  SECTION:=firmware
  CATEGORY:=Firmware
  TITLE:=AP6275P (BCM43752) PCIe firmware for brcmfmac
  DEPENDS:=+kmod-brcmfmac
endef

define Download/ap6275p-fw
  URL:=https://raw.githubusercontent.com/ophub/firmware/$(PKG_SOURCE_VERSION)/firmware/ap6275p/
  FILE:=fw_bcm43752a2_pcie_ag.bin
  HASH:=skip
endef

define Download/ap6275p-clm
  URL:=https://raw.githubusercontent.com/ophub/firmware/$(PKG_SOURCE_VERSION)/firmware/ap6275p/
  FILE:=clm_bcm43752a2_pcie_ag.blob
  HASH:=skip
endef

define Download/ap6275p-nvram
  URL:=https://raw.githubusercontent.com/ophub/firmware/$(PKG_SOURCE_VERSION)/firmware/ap6275p/
  FILE:=nvram_ap6275p.txt
  HASH:=skip
endef

$(eval $(call Download,ap6275p-fw))
$(eval $(call Download,ap6275p-clm))
$(eval $(call Download,ap6275p-nvram))

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)/firmware/ap6275p
	$(CP) $(DL_DIR)/fw_bcm43752a2_pcie_ag.bin \
		$(PKG_BUILD_DIR)/firmware/ap6275p/
	$(CP) $(DL_DIR)/clm_bcm43752a2_pcie_ag.blob \
		$(PKG_BUILD_DIR)/firmware/ap6275p/
	$(CP) $(DL_DIR)/nvram_ap6275p.txt \
		$(PKG_BUILD_DIR)/firmware/ap6275p/
endef

define Build/Compile
	true
endef

define Package/rkwifi-firmware-ap6275p/install
	$(INSTALL_DIR) $(1)/lib/firmware/brcm
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/firmware/ap6275p/fw_bcm43752a2_pcie_ag.bin \
		$(1)/lib/firmware/brcm/brcmfmac43752-pcie.bin
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/firmware/ap6275p/clm_bcm43752a2_pcie_ag.blob \
		$(1)/lib/firmware/brcm/brcmfmac43752-pcie.clm_blob
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/firmware/ap6275p/nvram_ap6275p.txt \
		$(1)/lib/firmware/brcm/brcmfmac43752-pcie.txt
endef

$(eval $(call BuildPackage,rkwifi-firmware-ap6275p))
