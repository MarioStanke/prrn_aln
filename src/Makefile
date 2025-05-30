#       Makefile.in for prrn/aln
#       Copyright(c) Osamu Gotoh <<o.gotoh@aist.go.jp>>
exec_prefix = /home/mario/tools/prrn_aln/src/../bin
table_dir =/home/mario/tools/prrn_aln/src/../table
alndbs_dir =/home/mario/tools/prrn_aln/src/../seqdb
CXX  = g++
CFLAGS = -O3
#CXX = clang++
#CFLAGS = -Wall
RANLIB = ranlib
LD  = ${CXX}
AR = ar rc
DEL = rm -f
DEFLT = -DSSHP=1 -DM_THREAD=1

CXX := $(CXX) $(CFLAGS) $(DEFLT)

.SUFFIXES: .o .cc .ccc .h .sh

PROG = aln iden phyln makmdm makdbs rdn utn utp upg nj decomp prrn5

STDH = stdtype.h
CLIB = clib.a -lpthread -lm -lz
HLIB = hblib.a $(CLIB)
SLIB = sblib.a $(CLIB)

.cc.o:
	$(CXX) -c $<
.ccc.o:
	$(CXX) -c $<

.cc:
	$(CXX) -o $@ $< $(CLIB)


all: $(PROG) 
prrn: prrn5

clean:
	$(DEL) $(PROG) *.exe
clear:
	$(DEL) $(PROG) *.exe *.o *.a
clearall:
	$(DEL) $(PROG) core *.o *.a *.exe *% *BAK Makefile iolib.h

tar:
	$(DEL) *.o *.a *% *BAK *~ Makefile iolib.h $(PROG)
	cd .. ; \
	Cur=`pwd` ; \
	Pnm=`basename $$Cur` ; \
	cd .. ; \
	tar cvf Sources.tar $$Pnm

install:
	test -d $(exec_prefix) || mkdir $(exec_prefix)
	cp $(PROG) $(exec_prefix)
	test -d $(table_dir) || mkdir $(table_dir)
	@if test "$(table_dir)" != "$(CURDIR)/../table"; then \
		cp -pfR ../table/????* $(table_dir); \
	fi
	./makmdm $(table_dir)
	test -d $(alndbs_dir) || mkdir $(alndbs_dir)
	@if test "$(alndbs_dir)" != "$(CURDIR)/../seqdb"; then \
		cp -pfR ../seqdb/????* $(alndbs_dir); \
	fi

install_prrn:
	test -e prrn5 && cp prrn5 $(exec_prefix)
	ln $(exec_prefix)/prrn5 $(exec_prefix)/prrn

uninstall uninst:
	cd $(exec_prefix); rm -f $(PROG)
	cd $(table_dir); rm -f $(TABLE)

test:   $(PROG)
	@if test -r $(table_dir)/mdm_mtx; then \
	  ./test.sh; \
	else \
	   echo "please make install before test"; \
	fi

wc:
	wc $(SRC)
ls:
	ls $(SRC)

aln:	aln.cc aln.h gaps.h vmf.h wln.h seq.h maln.h mgaps.h \
	mseq.h autocomp.h phyl.h fspscore.h $(HLIB)
	$(CXX) -o aln aln.cc $(HLIB)
iden:	iden.o autocomp.o $(SLIB)
	$(CXX) -o iden iden.o autocomp.o $(SLIB)
makdbs:	makdbs.cc makdbs.h dbs.h seq.h bitpat.h $(HLIB)
	$(CXX) -o makdbs makdbs.cc $(HLIB)
makmdm:	makmdm.cc mdm.h $(CLIB)
	$(CXX) -o makmdm makmdm.cc $(CLIB)
phyln:	phyl.cc phyl.h autocomp.h $(HLIB)
	$(CXX) -o phyln -DPHYL phyl.cc $(HLIB)
prrn5:	prrn5.o prrn5.h adjmat.o sltree.o blksrc.o fwd2b1.o $(HLIB)
	$(CXX) -o prrn5 prrn5.o adjmat.o sltree.o blksrc.o fwd2b1.o $(HLIB)
utp:	utp.o utilseq.o prs.o pattern.o $(HLIB)
	$(CXX) -o utp utp.o utilseq.o prs.o pattern.o $(HLIB)
utn:	utn.o extcds.o utilseq.o resite.o pattern.o $(HLIB)
	$(CXX) -o utn utn.o extcds.o utilseq.o resite.o pattern.o $(HLIB)
rdn:	rdn.o       $(HLIB)
	$(CXX) -o rdn rdn.o $(HLIB)
upg:	phyl.cc phyl.h $(HLIB)
	$(CXX) -o upg -DUPG phyl.cc $(HLIB)
nj:	phyl.cc phyl.h $(HLIB)
	$(CXX) -o nj -DNJ phyl.cc $(HLIB) 
decomp: decomp.cc $(SLIB)
	$(CXX) -o decomp decomp.cc $(SLIB)

aln.o:	aln.h vmf.h wln.h mseq.h maln.h mgaps.h autocomp.h phyl.h consreg.h fspscore.h
aln2.o:	aln2.cc	seq.h		aln.h
autocomp.o:	autocomp.cc autocomp.h $(STDH)
codepot.o:	codepot.cc	codepot.h
css.o:	css.cc css.h seq.h
dbs.o:	dbs.cc dbs.h $(STDH)
fspscore.o:	fspscore.cc	seq.h	aln.h	phyl.h	ssp.h
fwd2h1.o:	fwd2h1.cc	aln.h	seq.h	codepot.h
fwd2b1.o:	fwd2b1.cc	aln.h	seq.h
fwd2h.o:	fwd2h.h fwd2h.cc aln.h mseq.h maln.h gfreq.h vmf.h
fwd2s.o:	fwd2s.cc	fwd2s.h	aln.h	seq.h	codepot.h
fwd2c.o:	fwd2c.cc fwd2c.h aln.h maln.h seq.h
gaps.o:	    gaps.cc  gaps.h  seq.h
gfreq.o:    gfreq.cc	seq.h
gsinfo.o:	gsinfo.cc	gsinfo.h	seq.h		aln.h
mgaps.o:	mgaps.cc	seq.h aln.h mgaps.h gfreq.h
maln2.o:	maln2.cc fwd2h.cc fwd2h.h fwd2s.h fwd2c.h aln.h \
	maln.h seq.h mseq.h gfreq.h
maln2.o:	maln2.cc fwd2b.h aln.h maln.h seq.h
pattern.o:  pattern.cc	pattern.h
phyl.o:	phyl.cc phyl.h
prrn5.o:    prrn5.cc  prrn5.h gaps.h  seq.h	divseq.h
qdiv.o:	qdiv.cc aln.h wln.h utilseq.h bitpat.h qdiv.h
randiv.o:   randiv.cc	randiv.h    seq.h	divseq.h
resite.o:   resite.cc	resite.h    pattern.h	seq.h
simmtx.o:	simmtx.cc seq.h aln.h mdm.h
ssp.o:	ssp.cc	ssp.h	seq.h
sqpr.o:	sqpr.cc	seq.h		dbs.h	seq.h
seq.o:	seq.cc	seq.h		aln.h	dbs.h	seq.h
utilseq.o:	utilseq.cc	seq.h
vmf.o:	vmf.cc vmf.h $(STDH)
wln.o:	wln.cc	seq.h	    aln.h	wln.h
extcds.o:	extcds.cc extcds.h seq.h dbs.h makcds.h
prs.o:	prs.cc prs.h seq.h
adjmat.o:	adjmat.cc adjmat.h
sltree.o:	sltree.cc sltree.h adjmat.h
blksrc.o:	blksrc.cc blksrc.h

hblib.a: aln2.o autocomp.o codepot.o consreg.o css.o dbs.o \
	fspscore.o dpunit.o fwd2c.o fwd2d1.o fwd2h.o fwd2s.o \
	gaps.o gfreq.o gsinfo.o maln2.o mgaps.o mseq.o \
	pattern.o divseq.o phyl.o bitpat.o qdiv.o randiv.o utilseq.o \
	seq.o simmtx.o sqpr.o vmf.o wln.o ssp.o
	$(AR) hblib.a aln2.o autocomp.o codepot.o consreg.o css.o dbs.o \
	fspscore.o dpunit.o fwd2c.o fwd2d1.o fwd2h.o fwd2s.o \
	gaps.o gfreq.o gsinfo.o maln2.o mgaps.o mseq.o \
	pattern.o divseq.o  phyl.o bitpat.o qdiv.o randiv.o utilseq.o \
	seq.o simmtx.o sqpr.o vmf.o wln.o ssp.o
	$(RANLIB) hblib.a

sblib.a: aln2.o dbs.o gaps.o codepot.o bitpat.o \
	gsinfo.o divseq.o fwd2b1.o fwd2d1.o \
	sqpr.o simmtx.o seq.o utilseq.o vmf.o wln.o
	$(AR) sblib.a aln2.o dbs.o gaps.o codepot.o bitpat.o \
	gsinfo.o divseq.o fwd2b1.o fwd2d1.o \
	sqpr.o simmtx.o seq.o utilseq.o vmf.o wln.o
	$(RANLIB) sblib.a

clib.o:		clib.cc clib.h calcserv.h stdtype.h
iolib.o:	iolib.cc		stdtype.h
mfile.o:	mfile.cc		stdtype.h
sets.o:		sets.cc		stdtype.h
supprime.o:	supprime.cc	stdtype.h

clib.a: clib.o iolib.o mfile.o sets.o supprime.o calcserv.o
	$(AR) clib.a clib.o iolib.o mfile.o sets.o supprime.o calcserv.o
	$(RANLIB) clib.a

cmn.h:	$(STDH) 
	touch cmn.h
seq.h:	$(STDH)
	touch seq.h
