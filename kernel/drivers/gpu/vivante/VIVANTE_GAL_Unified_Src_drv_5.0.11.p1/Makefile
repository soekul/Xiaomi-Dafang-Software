

OS_KERNEL_DIR   := hal/os/linux/kernel
ARCH_KERNEL_DIR := hal/kernel/arch
ARCH_VG_KERNEL_DIR := hal/kernel/archvg
HAL_KERNEL_DIR  := hal/kernel

#VIV_DRIVER_PATH :=drivers/gpu/vivante/VIVANTE_GAL_Unified_Src_drv_5.0.11.p1
AQROOT :=drivers/gpu/vivante/VIVANTE_GAL_Unified_Src_drv_5.0.11.p1
PLATFORM :=m200/m200

ifdef CONFIG_VIVANTE_ENABLE_VG
VIVANTE_ENABLE_VG := 1
else
VIVANTE_ENABLE_VG := 0
endif



ifeq ($(VIVANTE_ENABLE_VG), 1)
EXTRA_CFLAGS += -DgcdENABLE_VG=1
else
EXTRA_CFLAGS += -DgcdENABLE_VG=0
endif


# CONFIG_GPU_DYNAMIC_CLOCK_POWER. If not define CONFIG_GPU_DYNAMIC_CLOCK_POWER, power on gpu module and enable gpu clock when drv_init().

### debug

### release
### The below EXTRA_CFLAGS are the same between building android and linux ###
EXTRA_CFLAGS += -DDBG=0


EXTRA_CFLAGS += -Werror -DLINUX -DDRIVER -DNO_DMA_COHERENT -DUSE_PLATFORM_DRIVER=1 -DVIVANTE_PROFILER=1 -DVIVANTE_PROFILER_CONTEXT=1 -DENABLE_GPU_CLOCK_BY_DRIVER=1 -DUSE_NEW_LINUX_SIGNAL=0 -DgcdPAGED_MEMORY_CACHEABLE=0 -DgcdNONPAGED_MEMORY_CACHEABLE=0 -DgcdNONPAGED_MEMORY_BUFFERABLE=1 -DgcdCACHE_FUNCTION_UNIMPLEMENTED=0 -DgcdSMP=0 -DgcdENABLE_OUTER_CACHE_PATCH=1 -DgcdFPGA_BUILD=0



obj-y += $(OS_KERNEL_DIR)/gc_hal_kernel_device.o \
        $(OS_KERNEL_DIR)/gc_hal_kernel_linux.o \
        $(OS_KERNEL_DIR)/gc_hal_kernel_math.o \
        $(OS_KERNEL_DIR)/gc_hal_kernel_os.o \
        $(OS_KERNEL_DIR)/gc_hal_kernel_debugfs.o \
        $(OS_KERNEL_DIR)/gc_hal_kernel_allocator.o \

ifneq ($(PLATFORM),)
obj-y += $(OS_KERNEL_DIR)/gc_hal_kernel_probe.o
obj-y += $(OS_KERNEL_DIR)/platform/$(PLATFORM).o
else
obj-y += $(OS_KERNEL_DIR)/gc_hal_kernel_driver.o
endif

obj-y += $(HAL_KERNEL_DIR)/gc_hal_kernel.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_command.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_db.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_debug.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_event.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_heap.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_mmu.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_video_memory.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_power.o

obj-y += $(ARCH_KERNEL_DIR)/gc_hal_kernel_context.o \
        $(ARCH_KERNEL_DIR)/gc_hal_kernel_hardware.o

ifeq ($(VIVANTE_ENABLE_VG), 1)
obj-y +=\
          $(HAL_KERNEL_DIR)/gc_hal_kernel_vg.o\
          $(HAL_KERNEL_DIR)/gc_hal_kernel_command_vg.o\
          $(HAL_KERNEL_DIR)/gc_hal_kernel_interrupt_vg.o\
          $(HAL_KERNEL_DIR)/gc_hal_kernel_mmu_vg.o\
          $(ARCH_VG_KERNEL_DIR)/gc_hal_kernel_hardware_command_vg.o\
          $(ARCH_VG_KERNEL_DIR)/gc_hal_kernel_hardware_vg.o
endif

ifneq ($(CONFIG_SYNC),)
EXTRA_CFLAGS += -Idrivers/staging/android

obj-y += $(OS_KERNEL_DIR)/gc_hal_kernel_sync.o
endif

ifeq ($(SECURITY), 1)
obj-y += $(OS_KERNEL_DIR)/gc_hal_kernel_security_channel.o \
        $(HAL_KERNEL_DIR)/gc_hal_kernel_security.o
endif


EXTRA_CFLAGS += -I$(AQROOT)/hal/kernel/inc
EXTRA_CFLAGS += -I$(AQROOT)/hal/kernel
EXTRA_CFLAGS += -I$(AQROOT)/hal/kernel/arch
EXTRA_CFLAGS += -I$(AQROOT)/hal/kernel/inc
EXTRA_CFLAGS += -I$(AQROOT)/hal/os/linux/kernel

ifeq ($(VIVANTE_ENABLE_VG), 1)
EXTRA_CFLAGS += -I$(AQROOT)/hal/kernel/archvg
endif
