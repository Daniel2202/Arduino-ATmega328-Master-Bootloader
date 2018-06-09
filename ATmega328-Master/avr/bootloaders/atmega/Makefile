# Makefile for ATmegaBOOT
# E.Lins, modified by Daniel Ulrich, 2018

# program name should not be changed...
PROGRAM    = ATmegaBOOT_168

# enter the parameters for the avrdude isp tool
ISPTOOL	   = stk500v2
ISPPORT	   = usb
ISPSPEED   = -b 115200

MCU_TARGET = atmega168
LDSECTION  = --section-start=.text=0x3800

# the efuse should really be 0xf8; since, however, only the lower
# three bits of that byte are used on the atmega168, avrdude gets
# confused if you specify 1's for the higher bits, see:
# http://tinker.it/now/2007/02/24/the-tale-of-avrdude-atmega168-and-extended-bits-fuses/
#
# similarly, the lock bits should be 0xff instead of 0x3f (to
# unlock the bootloader section) and 0xcf instead of 0x0f (to
# lock it), but since the high two bits of the lock byte are
# unused, avrdude would get confused.

ISPFUSES    = avrdude -c $(ISPTOOL) -p $(MCU_TARGET) -P $(ISPPORT) $(ISPSPEED) \
-e -u -U lock:w:0x3f:m -U efuse:w:0x$(EFUSE):m -U hfuse:w:0x$(HFUSE):m -U lfuse:w:0x$(LFUSE):m
ISPFLASH    = avrdude -c $(ISPTOOL) -p $(MCU_TARGET) -P $(ISPPORT) $(ISPSPEED) \
-U flash:w:$(PROGRAM)_$(TARGET).hex -U lock:w:0x0f:m

STK500 = "C:\Program Files\Atmel\AVR Tools\STK500\Stk500.exe"
STK500-1 = $(STK500) -e -d$(MCU_TARGET) -pf -vf -if$(PROGRAM)_$(TARGET).hex \
-lFF -LFF -f$(HFUSE)$(LFUSE) -EF8 -ms -q -cUSB -I200kHz -s -wt
STK500-2 = $(STK500) -d$(MCU_TARGET) -ms -q -lCF -LCF -cUSB -I200kHz -s -wt


OBJ        = $(PROGRAM).o
OPTIMIZE   = -Os

DEFS       =
LIBS       =

CC         = avr-gcc

# Override is only needed by avr-lib build system.

override CFLAGS        = -g -Wall $(OPTIMIZE) -mmcu=$(MCU_TARGET) -DF_CPU=$(AVR_FREQ) $(DEFS)
override LDFLAGS       = -Wl,$(LDSECTION)
#override LDFLAGS       = -Wl,-Map,$(PROGRAM).map,$(LDSECTION)

OBJCOPY        = avr-objcopy
OBJDUMP        = avr-objdump

all:

atmega328_1MHz: TARGET = atmega328_pro_1MHz
atmega328_1MHz: MCU_TARGET = atmega328p
atmega328_1MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=9600
atmega328_1MHz: AVR_FREQ = 1000000L
atmega328_1MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_1MHz: $(PROGRAM)_atmega328_1MHz.hex

atmega328_7MHz: TARGET = atmega328_pro_7MHz
atmega328_7MHz: MCU_TARGET = atmega328p
atmega328_7MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=115200
atmega328_7MHz: AVR_FREQ = 7372800L
atmega328_7MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_7MHz: $(PROGRAM)_atmega328_7MHz.hex

atmega328_8MHz: TARGET = atmega328_pro_8MHz
atmega328_8MHz: MCU_TARGET = atmega328p
atmega328_8MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=38400
atmega328_8MHz: AVR_FREQ = 8000000L
atmega328_8MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_8MHz: $(PROGRAM)_atmega328_8MHz.hex

atmega328_11MHz: TARGET = atmega328_pro_11MHz
atmega328_11MHz: MCU_TARGET = atmega328p
atmega328_11MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=115200
atmega328_11MHz: AVR_FREQ = 11059200L
atmega328_11MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_11MHz: $(PROGRAM)_atmega328_11MHz.hex

atmega328_14MHz: TARGET = atmega328_pro_14MHz
atmega328_14MHz: MCU_TARGET = atmega328p
atmega328_14MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=115200
atmega328_14MHz: AVR_FREQ = 14745600L
atmega328_14MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_14MHz: $(PROGRAM)_atmega328_14MHz.hex

atmega328_16MHz: TARGET = atmega328_pro_16MHz
atmega328_16MHz: MCU_TARGET = atmega328p
atmega328_16MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=38400
atmega328_16MHz: AVR_FREQ = 16000000L
atmega328_16MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_16MHz: $(PROGRAM)_atmega328_16MHz.hex

atmega328_18MHz: TARGET = atmega328_pro_18MHz
atmega328_18MHz: MCU_TARGET = atmega328p
atmega328_18MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=115200
atmega328_18MHz: AVR_FREQ = 18432000L
atmega328_18MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_18MHz: $(PROGRAM)_atmega328_18MHz.hex

atmega328_20MHz: TARGET = atmega328_pro_20MHz
atmega328_20MHz: MCU_TARGET = atmega328p
atmega328_20MHz: CFLAGS += '-DMAX_TIME_COUNT=F_CPU>>4' '-DNUM_LED_FLASHES=1' -DBAUD_RATE=115200
atmega328_20MHz: AVR_FREQ = 20000000L
atmega328_20MHz: LDSECTION  = --section-start=.text=0x7800
atmega328_20MHz: $(PROGRAM)_atmega328_20MHz.hex

isp: $(TARGET)
	$(ISPFUSES)
	$(ISPFLASH)

isp-stk500: $(PROGRAM)_$(TARGET).hex
	$(STK500-1)
	$(STK500-2)

%.elf: $(OBJ)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $^ $(LIBS)

clean:
	rm -rf *.o *.elf *.lst *.map *.sym *.lss *.eep *.srec *.bin *.hex

%.lst: %.elf
	$(OBJDUMP) -h -S $< > $@

%.hex: %.elf
	$(OBJCOPY) -j .text -j .data -O ihex $< $@

%.srec: %.elf
	$(OBJCOPY) -j .text -j .data -O srec $< $@

%.bin: %.elf
	$(OBJCOPY) -j .text -j .data -O binary $< $@
	
