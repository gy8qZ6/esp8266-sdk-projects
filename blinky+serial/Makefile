CC = xtensa-lx106-elf-gcc
CFLAGS = -I. -mlongcalls
LDLIBS = -nostdlib -Wl,--start-group -lmain -lnet80211 -lwpa -llwip -lpp -lphy -lc -Wl,--end-group -lgcc
LDFLAGS = -Teagle.app.v6.ld

blinky-0x00000.bin: blinky
	esptool.py elf2image $^

blinky.o: blinky.c

blinky: blinky.o driver/uart.o
	$(CC) $(LDFLAGS) $^ -o $@ $(LDLIBS)

flash: blinky-0x00000.bin
	esptool.py write_flash 0 blinky-0x00000.bin 0x10000 blinky-0x10000.bin

clean:
	rm -f blinky blinky.o blinky-0x00000.bin blinky-0x10000.bin
