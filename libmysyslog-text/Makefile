CC = gcc
CFLAGS = -fPIC -I../libmysyslog/include
AR = ar
ARFLAGS = rcs

SRC = src/libmysyslog-text.c
OBJ = $(SRC:.c=.o)
LIB_SHARED = libmysyslog-text.so
LIB_STATIC = libmysyslog-text.a
DEB_DIR = libmysyslog-text_deb

all: $(LIB_SHARED) $(LIB_STATIC)

$(LIB_SHARED): $(OBJ)
	$(CC) -shared -o $@ $^

$(LIB_STATIC): $(OBJ)
	$(AR) $(ARFLAGS) $@ $^

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) $(LIB_SHARED) $(LIB_STATIC)
	rm -f *.deb

deb: all
	mkdir -p $(DEB_DIR)/DEBIAN $(DEB_DIR)/usr/lib
	echo "Package: libmysyslog-text" > $(DEB_DIR)/DEBIAN/control
	echo "Version: 1.0" >> $(DEB_DIR)/DEBIAN/control
	echo "Section: libs" >> $(DEB_DIR)/DEBIAN/control
	echo "Priority: optional" >> $(DEB_DIR)/DEBIAN/control
	echo "Architecture: amd64" >> $(DEB_DIR)/DEBIAN/control
	echo "Maintainer: AACnotAliVe <mrlenorgenri@gmail.com>" >> $(DEB_DIR)/DEBIAN/control
	echo "Depends: libmysyslog" >> $(DEB_DIR)/DEBIAN/control
	echo "Description: Text format driver for mysyslog" >> $(DEB_DIR)/DEBIAN/control
	cp $(LIB_SHARED) $(DEB_DIR)/usr/lib/
	dpkg-deb --build $(DEB_DIR)
	rm -r $(DEB_DIR)
