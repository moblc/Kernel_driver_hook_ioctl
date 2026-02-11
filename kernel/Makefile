MODULE_NAME := kerneldriver
RESMAN_CORE_OBJS := entry.o
ccflags-y += -Wno-macro-redefined -Wno-declaration-after-statement -Wno-unused-function -fvisibility=hidden
ifneq ($(KERNELRELEASE),)    
	obj-m := $(MODULE_NAME).o
	$(MODULE_NAME)-objs:=$(RESMAN_CORE_OBJS)
else
RESMAN_GLUE_OBJS:=
	KDIR := /workspaces/Kernel_driver_hook_ioctl/android-kernel/out/android13-5.10
all:
	make -j$(nproc) -C $(KDIR) M=$(shell pwd) LLVM=1 LLVM_IAS=1 ARCH=arm64 CC=clang LD=ld.lld OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump NM=llvm-nm STRIP=llvm-strip modules
	rm -rf *.o .*.ko.cmd .*.o.cmd *.mod.o *.mod.c *.symvers *.order .tmp_versions .*.mod.cmd *.mod
	llvm-strip --strip-debug $(MODULE_NAME).ko
clean:    
	rm -f *.ko *.o *.mod.o *.mod.c *.symvers *.order
endif
