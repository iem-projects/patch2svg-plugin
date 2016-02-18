
PACKAGE_NAME = patch to SVG
PACKAGE_VERSION = 1.0
TCLFILES = patch2svg-plugin.tcl

# we use all language files found here
POFILES=$(wildcard *.po)
MSGFILES=$(POFILES:.po=.msg)

TEMPLATE = patch2svg.pot
FILES = $(addprefix ../, $(TCLFILES))

# generate .msg files from the .po files
all: $(TEMPLATE) $(MSGFILES)

# refresh .po files from the template
clean:
	-rm -f -- $(MSGFILES)
	-rm -f -- $(POFILES:=~)
	-rm -f -- $(TEMPLATE)
distclean: clean

po: $(TEMPLATE) $(POFILES)

$(TEMPLATE): $(FILES)
	touch $(TEMPLATE)
	xgettext --join-existing \
		--from-code=UTF-8 --language=Tcl --keyword=_ \
		--sort-output --no-location --output=$(TEMPLATE) \
		--package-name="$(PACKAGE_NAME)" \
		--package-version=$(PACKAGE_VERSION) \
		--copyright-holder='This file is put in the public domain' \
		--foreign-user \
		--msgid-bugs-address=http://bugs.puredata.info \
		$(FILES)

$(POFILES): $(TEMPLATE)
	touch $@
	msgmerge --sort-output --no-fuzzy-matching --no-location --update $@ $(TEMPLATE)

%.msg: %.po
	msgfmt --check --tcl --locale=$* -d . $<


#install: $(MSGFILES)
#	install -d $(DESTDIR)
#	install $(MSGFILES) $(DESTDIR)
install:
	@echo "nothing to install"
