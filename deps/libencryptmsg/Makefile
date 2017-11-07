.PHONY: src tests cli gtest symlinks clean-symlinks
all: src cli
gtest:
	$(MAKE) -C tests -f Makefile.gtest RELEASE=$(RELEASE)

tests: gtest src
	$(MAKE) -C tests RELEASE=$(RELEASE)
	$(MAKE) -C test_assets RELEASE=$(RELEASE)

cli: src
	$(MAKE) -C cli RELEASE=$(RELEASE)

src: symlinks
	$(MAKE) -C src RELEASE=$(RELEASE)

clean: clean-children | clean-symlinks
clean-children:
	$(MAKE) -C tests -f Makefile.gtest clean RELEASE=$(RELEASE)
	$(MAKE) -C tests clean RELEASE=$(RELEASE)
	$(MAKE) -C cli clean RELEASE=$(RELEASE)
	$(MAKE) -C src clean RELEASE=$(RELEASE)
	$(MAKE) -C test_assets clean RELEASE=$(RELEASE)

LNDIRNAME=makefiles stlplus gtest
LNDIR=$(LNDIRNAME:%=deps/%)
CLEANLNDIR=$(LNDIR:%=clean-%)

.PHONY: $(CLEANLNDIR)

symlinks: $(LNDIR)

clean-symlinks: $(CLEANLNDIR)

$(LNDIR):
	ln -s ../../$(@:deps/%=%) deps/

$(CLEANLNDIR):
	rm $(@:clean-%=%)