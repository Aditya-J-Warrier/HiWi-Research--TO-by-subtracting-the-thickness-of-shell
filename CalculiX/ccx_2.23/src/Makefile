CFLAGS = -Wall -O2 -DARCH="Linux" -DMATRIXSTORAGE -DNETWORKOUT
FFLAGS = -Wall -O2 -cpp 

CC=cc
FC=gfortran

.c.o :
	$(CC) $(CFLAGS) -c $<
.f.o :
	$(FC) $(FFLAGS) -c $<

include Makefile.inc

SCCXMAIN = ccx_2.23.c

OCCXF = $(SCCXF:.f=.o)
OCCXC = $(SCCXC:.c=.o)
OCCXMAIN = $(SCCXMAIN:.c=.o)

DIR=../../../SPOOLES.2.2

EXTRA_OBJS = feasibledirection.o randomfieldmain.o filterbackwardmain.o filterforwardmain.o

LIBS = $(EXTRA_OBJS) -llapack -lblas -lpthread -lm -lc

ccx_2.23: $(OCCXMAIN) ccx_2.23.a $(EXTRA_OBJS)
	./date.pl; $(CC) $(CFLAGS) -c ccx_2.23.c; $(FC) -Wall -O2 -o $@ $(OCCXMAIN) ccx_2.23.a $(LIBS) -fopenmp

ccx_2.23.a: $(OCCXF) $(OCCXC)
	ar vr $@ $?
