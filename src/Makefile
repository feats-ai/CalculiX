
CFLAGS = -Wall -O2  -I ../SPOOLES.2.2 -DARCH="Linux" -DSPOOLES -DARPACK -DMATRIXSTORAGE -DNETWORKOUT
FFLAGS = -Wall -O2

CC=gcc
FC=gfortran

.c.o :
	$(CC) $(CFLAGS) -c $<
.f.o :
	$(FC) $(FFLAGS) -c $<

include Makefile.inc

SCCXMAIN = CalculiX.c

OCCXF = $(SCCXF:.f=.o)
OCCXC = $(SCCXC:.c=.o)
OCCXMAIN = $(SCCXMAIN:.c=.o)

DIR=../SPOOLES.2.2

LIBS = \
       $(DIR)/spooles.a \
        /work/projects/project02298/.conda/envs/ccx/lib/libarpack.a\
	/work/projects/project02298/.conda/envs/ccx/lib/liblapack.a\
	/work/projects/project02298/.conda/envs/ccx/lib/libblas.a\
       -lpthread -lm -lc

CalculiX: $(OCCXMAIN) CalculiX.a  $(LIBS)
	./date.pl; $(CC) $(CFLAGS) -c CalculiX.c; $(FC)  -Wall -O2 -o $@ $(OCCXMAIN) CalculiX.a $(LIBS) -fopenmp

CalculiX.a: $(OCCXF) $(OCCXC)
	ar vr $@ $?
