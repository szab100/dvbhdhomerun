KERNEL_VERSION	:= `uname -r`
KERNEL_DIR	:= /lib/modules/$(KERNEL_VERSION)/build

PWD		:= $(shell pwd)

EXTRA_CFLAGS += -Idrivers/media/dvb/dvb-core/ -Idrivers/media/dvb/frontends

dvb_hdhomerun-objs := dvb_hdhomerun_init.o dvb_hdhomerun_data.o dvb_hdhomerun_control.o
obj-m += dvb_hdhomerun.o

#dvb_hdhomerun_core-objs := dvb_hdhomerun_core.o
obj-m += dvb_hdhomerun_core.o

#dvb_hdhomerun_fe-objs := dvb_hdhomerun_fe.o
obj-m += dvb_hdhomerun_fe.o

all: dvb_hdhomerun
dvb_hdhomerun:
	@echo "Building driver..."
	$(MAKE) -C $(KERNEL_DIR) SUBDIRS=$(PWD) modules

install:
	$(MAKE) -C $(KERNEL_DIR) SUBDIRS=$(PWD) modules_install
	depmod -aeF /boot/System.map-$(KERNEL_VERSION)

clean:
	rm -f *~
	rm -f Module.symvers Module.markers modules.order
	$(MAKE) -C $(KERNEL_DIR) M=$(PWD) clean