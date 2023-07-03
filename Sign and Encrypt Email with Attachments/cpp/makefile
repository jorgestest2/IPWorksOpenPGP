# 
# IPWorks OpenPGP 2022 C++ Edition - Sample Project
# 
# This sample project demonstrates the usage of IPWorks OpenPGP in a 
# simple, straightforward way. This is not intended to be a complete 
# application. Error handling and other checks are simplified for clarity.
# 
# Copyright (c) 2023 /n software inc. www.nsoftware.com
# 

ifeq ($(shell uname -s), Darwin) # MACOS
R_PATH=-Wl,-rpath,../../lib64/,-rpath,.

FRAMEWORK = -framework Carbon -framework Security
LD_FLAGS = -lipworksopenpgp.22.0 -L../../lib64/ -lresolv
LD_FLAGS_SRC = -lz -lresolv
OS_CFLAGS = -D UNIX -arch arm64
MACOS = "darwin% Darwin% macos%"

all:
	g++ $(OS_CFLAGS) -D UNIX -o pfilemailer pfilemailer.cpp  -I../../include/ $(LD_FLAGS) $(FRAMEWORK) $(R_PATH)

src: ../../src/ipworksopenpgp.o
	g++ $(OS_CFLAGS) -o pfilemailer ../../src/ipworksopenpgp.o pfilemailer.cpp  $(LD_FLAGS_SRC) $(FRAMEWORK)

../../src/ipworksopenpgp.o:
	g++ -c -fno-exceptions -fno-rtti -fPIC -arch arm64 -o ../../src/ipworksopenpgp.o ../../src/ipworksopenpgp.cpp

else # LINUX
ifeq ($(shell uname -m), x86_64)
  LIB=lib64
else
  LIB=lib
endif

R_PATH=-Wl,-rpath,../../$(LIB)/,-rpath,.
LD_FLAGS = -lipworksopenpgp  -L../../$(LIB)/ 
LD_FLAGS_SRC = -lz 

all:
	g++ -D UNIX -o pfilemailer pfilemailer.cpp  -I../../include/ $(LD_FLAGS) $(R_PATH) 

src: ../../src/ipworksopenpgp.o
	g++ -D UNIX -o pfilemailer ../../src/ipworksopenpgp.o pfilemailer.cpp  -I../../include/ $(LD_FLAGS_SRC)

../../src/ipworksopenpgp.o:
	g++ -c -fno-exceptions -fno-rtti -fPIC -o ../../src/ipworksopenpgp.o ../../src/ipworksopenpgp.cpp

clean:
	rm -f ../../src/*.o
	rm -f pfilemailer *.o
endif