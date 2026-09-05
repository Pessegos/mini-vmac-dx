CC ?= gcc
WINDRES ?= windres

TARGET = minivmac-plus.exe
OBJDIR = bld

CFLAGS_COMMON = -Wall -Wmissing-prototypes -Wno-uninitialized -Wundef -Wstrict-prototypes -Icfg -Isrc
CFLAGS = -O2 $(CFLAGS_COMMON)
LDFLAGS = -mwindows
LDLIBS = -ld3d9 -lwinmm -lole32 -luuid

OBJS = \
	$(OBJDIR)/MINEM68K.o \
	$(OBJDIR)/OSGLUWIN.o \
	$(OBJDIR)/GLOBGLUE.o \
	$(OBJDIR)/M68KITAB.o \
	$(OBJDIR)/VIAEMDEV.o \
	$(OBJDIR)/VIA2EMDV.o \
	$(OBJDIR)/IWMEMDEV.o \
	$(OBJDIR)/SCCEMDEV.o \
	$(OBJDIR)/RTCEMDEV.o \
	$(OBJDIR)/ROMEMDEV.o \
	$(OBJDIR)/SCSIEMDV.o \
	$(OBJDIR)/SONYEMDV.o \
	$(OBJDIR)/SCRNEMDV.o \
	$(OBJDIR)/VIDEMDEV.o \
	$(OBJDIR)/MOUSEMDV.o \
	$(OBJDIR)/ADBEMDEV.o \
	$(OBJDIR)/ASCEMDEV.o \
	$(OBJDIR)/PROGMAIN.o

.PHONY: all clean

all: $(TARGET)

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(OBJDIR)/%.o: src/%.c cfg/CNFGGLOB.h | $(OBJDIR)
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJDIR)/main.res: cfg/main.rc cfg/app.manifest | $(OBJDIR)
	$(WINDRES) -i cfg/main.rc --input-format=rc -o $@ -O coff --include-dir cfg --include-dir src

$(TARGET): $(OBJS) $(OBJDIR)/main.res
	$(CC) -o $@ $(OBJS) $(OBJDIR)/main.res $(LDFLAGS) $(LDLIBS)

clean:
	rm -f $(OBJS) $(OBJDIR)/main.res $(TARGET)
