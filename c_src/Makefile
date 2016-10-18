LINUX=$(shell uname | grep Linux | wc -l | xargs echo)
DEPS=../deps

ifeq ($(LINUX),1)
ZMQ_FLAGS=--with-pic
else
ZMQ_FLAGS=
endif

ifndef ZEROMQ_VERSION
ZEROMQ_VERSION=3.2.2
endif

all: $(DEPS)/zeromq3/src/.libs/libzmq.a

clean:
	if test -e $(DEPS)/zeromq3/Makefile; then \
		cd $(DEPS)/zeromq3; make clean; \
	else \
		true; \
	fi

distclean:
	@rm -rf $(DEPS)

$(DEPS)/zeromq3:
	@mkdir -p $(DEPS)
	@curl http://pkgs.fedoraproject.org/repo/pkgs/zeromq3/zeromq-$(ZEROMQ_VERSION).tar.gz/df68431d9300da84a1a5f9a2784e33de/zeromq-$(ZEROMQ_VERSION).tar.gz -o $(DEPS)/zeromq-$(ZEROMQ_VERSION).tar.gz
	@cd $(DEPS) && tar xzvfp zeromq-$(ZEROMQ_VERSION).tar.gz && mv zeromq-$(ZEROMQ_VERSION) zeromq3


$(DEPS)/zeromq3/src/.libs/libzmq.a: $(DEPS)/zeromq3
	@cd $(DEPS)/zeromq3 && ./configure $(ZMQ_FLAGS) && make
