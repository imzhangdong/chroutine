CPP	= @echo " g++ $@"; g++
CC	= @echo " gcc $@"; gcc
LD	= @echo " ld  $@"; ld
AR	= @echo " ar  $@"; ar
RM	= @echo " RM	$@"; rm -f

CFLAGS += -Wall -std=c++11 -DENABLE_HTTP_PLUGIN -DDEBUG_BUILD
CFLAGS += -g

#LDFLAGS += "-Wl" -lpthread -lc
LDFLAGS += -lcurl
LDFLAGS += -L.  ##-lenc -lsyslink  -lbinder -llog    -losa -lpdi -lsdk  -lz -lrt -lsplice -lmem -ldec
AFLAGS += -r

INC = -I../../engin -I../../net/http_client -I../../util -I../../vendors

BINDIR = .
SRCDIR = . ../../engin ../../net/http_client  ../../util


SRCS_PATH = $(SRCDIR) 

LIB_SRCS += $(foreach dir,$(SRCS_PATH),$(wildcard $(dir)/*.cpp))
LIB_CC_SRCS += $(foreach dir,$(SRCS_PATH),$(wildcard $(dir)/*.cc))

LIB_OBJS += $(patsubst %.cpp,%.o,$(LIB_SRCS))
LIB_OBJS += $(patsubst %.cc,%.o,$(LIB_CC_SRCS))

LIB_APP = curltest.a

DEMO_NAME	= curltest
TARGET_DEMO = $(BINDIR)/$(DEMO_NAME)

all: $(TARGET_DEMO)

$(TARGET_DEMO) : $(LIB_APP)
	$(CPP) -o $@ $(LDFLAGS) $(INC) $^

$(LIB_APP): $(LIB_OBJS)
	$(RM) $@;
	$(AR) $(AFLAGS) $@ $^

.c.o:
	$(CC) -c $(CFLAGS) $(INC) $^ -o $@

.cpp.o:
	$(CPP) -c $(CFLAGS) $(INC) $^ -o $@

clean:
	$(RM) $(LIB_OBJS) $(LIB_APP) $(TARGET_DEMO)

cleanobj:
	$(RM) $(LIB_OBJS)