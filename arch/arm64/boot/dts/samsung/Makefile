ifeq ($(CONFIG_BUILD_ARM64_DT_OVERLAY),y)

ifeq ($(filter y,$(CONFIG_SEC_A70Q_PROJECT)),y)
# A70Q(SM6150)
SEC_A70Q_EUR_DTBO := \
                sm6150-sec-a70q-eur-overlay-r00.dtbo \
                sm6150-sec-a70q-eur-overlay-r01.dtbo \
				sm6150-sec-a70q-eur-overlay-r02.dtbo \
				sm6150-sec-a70q-eur-overlay-r03.dtbo \
				sm6150-sec-a70q-eur-overlay-r05.dtbo \
				sm6150-sec-a70q-eur-overlay-r06.dtbo \
				sm6150-sec-a70q-eur-overlay-r09.dtbo \
				sm6150-sec-a70q-eur-overlay-r10.dtbo \
				sm6150-sec-a70q-eur-overlay-r11.dtbo \
				sm6150-sec-a70q-eur-overlay-r12.dtbo \
				sm6150-sec-a70q-eur-overlay-r13.dtbo \
				sm6150-sec-a70q-eur-overlay-r14.dtbo
else ifeq ($(filter y,$(CONFIG_SEC_A70S_PROJECT)),y)
# A70S(SM6150)				
SEC_A70S_SWA_DTBO := \
				sm6150-sec-a70s-swa-overlay-r00.dtbo \
				sm6150-sec-a70s-swa-overlay-r01.dtbo
endif

define __sec_dtbo_build
dtbo-$(2) += $(1)
$(1)-base := $(3)
endef

define sec_dtbo_build
$(foreach dtbo, $(1), $(eval $(call __sec_dtbo_build, $(dtbo),$(2),$(3))))
endef

# SM6150 BASE DTB
SEC_SM6150_BASE_DTB := ../qcom/sm6150.dtb

ifeq ($(filter y,$(CONFIG_SEC_A70Q_PROJECT)),y)
$(eval $(call sec_dtbo_build, \
		$(SEC_A70Q_EUR_DTBO),$(CONFIG_SEC_A70Q_EUR_PROJECT),$(SEC_SM6150_BASE_DTB)))
else ifeq ($(filter y,$(CONFIG_SEC_A70S_PROJECT)),y)
$(eval $(call sec_dtbo_build, \
		$(SEC_A70S_SWA_DTBO),$(CONFIG_SEC_A70S_SWA_PROJECT),$(SEC_SM6150_BASE_DTB)))
endif
endif

ifeq ($(CONFIG_ARM64),y)
always          := $(dtb-y)
subdir-y        := $(dts-dirs)
else
targets += dtbs
targets += $(addprefix ../, $(dtb-y))

$(obj)/../%.dtb: $(src)/%.dts FORCE
        $(call if_changed_dep,dtc)

dtbs: $(addprefix $(obj)/../,$(dtb-y))
endif

clean-files := *.dtb *.dtbo
