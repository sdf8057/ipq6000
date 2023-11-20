include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Device/Default
	PROFILES := Default
	KERNEL_DEPENDS = $$(wildcard $(DTS_DIR)/$$(DEVICE_DTS).dts)
	KERNEL_INITRAMFS_PREFIX := $$(IMG_PREFIX)-$(1)-initramfs
	KERNEL_PREFIX := $$(IMAGE_PREFIX)
	KERNEL_LOADADDR := 0x41080000
	DEVICE_DTS_DIR := $(DTS_DIR)/qcom
	SUPPORTED_DEVICES := $(subst _,$(comma),$(1))
	IMAGE/sysupgrade.bin = sysupgrade-tar | append-metadata
	IMAGE/sysupgrade.bin/squashfs :=
endef

define Device/FitImage
	KERNEL_SUFFIX := -fit-uImage.itb
	KERNEL = kernel-bin | gzip | fit gzip $$(DEVICE_DTS_DIR)/$$(DEVICE_DTS).dtb
	KERNEL_NAME := Image
endef

define Device/FitImageLzma
	KERNEL_SUFFIX := -fit-uImage.itb
	KERNEL = kernel-bin | lzma | fit lzma $$(DEVICE_DTS_DIR)/$$(DEVICE_DTS).dtb
	KERNEL_NAME := Image
endef

define Device/UbiFit
	KERNEL_IN_UBI := 1
	IMAGES := nand-factory.ubi nand-sysupgrade.bin
	IMAGE/nand-factory.ubi := append-ubi
	IMAGE/nand-sysupgrade.bin := sysupgrade-tar | append-metadata
endef

define Device/cmiot_ax18
	$(call Device/FitImage)
	$(call Device/UbiFit)
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS := qcom-ipq6018-ax18
	DEVICE_DTS_CONFIG := config@cp03-c1
	DEVICE_TITLE := CMIOT AX18
	DEVICE_PACKAGES := kmod-usb3 kmod-usb-phy-msm
endef
TARGET_DEVICES += cmiot_ax18

define Device/glinet_gl-common
	$(call Device/FitImage)
	$(call Device/UbiFit)
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS_CONFIG := config@cp03-c1
	DEVICE_PACKAGES := kmod-usb3 kmod-usb-phy-msm
endef

define Device/glinet_gl-ax1800
	$(call Device/glinet_gl-common)
	DEVICE_DTS := qcom-ipq6018-gl-ax1800
	DEVICE_TITLE := GL.iNet GL-AX1800
	DEVICE_PACKAGES := ath11k-wifi-gl-axt1800
	IMAGES += nand-factory.bin
	IMAGE/nand-factory.bin := append-ubi | qsdk-ipq-factory-nand
	DEVICE_PACKAGES += ath11k-wifi-gl-ax1800
endef
TARGET_DEVICES += glinet_gl-ax1800

define Device/glinet_gl-axt1800
	$(call Device/glinet_gl-common)
	DEVICE_DTS := qcom-ipq6018-gl-axt1800
	DEVICE_TITLE := GL.iNet GL-AXT1800
	DEVICE_PACKAGES += ath11k-wifi-gl-axt1800 kmod-hwmon-pwmfan
endef
TARGET_DEVICES += glinet_gl-axt1800

define Device/huasifei_wf-hr6001
	$(call Device/FitImage)
	$(call Device/UbiFit)
  BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS := qcom-ipq6018-wf-hr6001
	DEVICE_DTS_CONFIG := config@cp01-c1
	DEVICE_TITLE := HUASIFEI WF-HR6001
endef
TARGET_DEVICES += huasifei_wf-hr6001

define Device/linksys_mr7350
	$(call Device/FitImage)
	KERNEL_SIZE := 8192k
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	UBINIZE_OPTS := -E 5
	IMAGES := factory.bin sysupgrade.bin
	IMAGE/factory.bin := append-kernel | pad-to $$$$(KERNEL_SIZE) | \
		append-ubi | linksys-image type=MR7350
	DEVICE_TITLE := Linksys MR7350
	DEVICE_DTS := qcom-ipq6018-mr7350
	DEVICE_PACKAGES := kmod-leds-pca963x kmod-usb3 \
		kmod-usb-ledtrig-usbport kmod-usb-phy-msm
endef
TARGET_DEVICES += linksys_mr7350

define Device/qihoo_v6
	$(call Device/FitImage)
	$(call Device/UbiFit)
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS := qcom-ipq6018-qihoo-v6
	DEVICE_DTS_CONFIG := config@cp03-c1
	DEVICE_TITLE := Qihoo V6
	DEVICE_PACKAGES := kmod-usb3 kmod-usb-phy-msm
endef
TARGET_DEVICES += qihoo_v6

define Device/xiaomi_rm1800
	$(call Device/FitImage)
	$(call Device/UbiFit)
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS := qcom-ipq6018-rm1800
	DEVICE_DTS_CONFIG := config@cp03-c1
	DEVICE_TITLE := Xiaomi RM1800
endef
TARGET_DEVICES += xiaomi_rm1800

define Device/redmi_ax5
	$(call Device/FitImage)
	$(call Device/UbiFit)
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS := qcom-ipq6018-ax5
	DEVICE_DTS_CONFIG := config@cp03-c1
	DEVICE_TITLE := Redmi AX5
endef
TARGET_DEVICES += redmi_ax5

define Device/zn_m2
	$(call Device/FitImage)
	$(call Device/UbiFit)
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	DEVICE_DTS := qcom-ipq6018-zn-m2
	DEVICE_DTS_CONFIG := config@cp03-c1
	DEVICE_TITLE := ZN M2
	DEVICE_PACKAGES := kmod-usb3 kmod-usb-phy-msm
endef
TARGET_DEVICES += zn_m2

$(eval $(call BuildImage))
