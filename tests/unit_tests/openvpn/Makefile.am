AUTOMAKE_OPTIONS = foreign

EXTRA_DIST = input

AM_TESTSUITE_SUMMARY_HEADER = ' for $(PACKAGE_STRING) Unit-Tests'

test_binaries=

if HAVE_LD_WRAP_SUPPORT
test_binaries += argv_testdriver buffer_testdriver
endif

test_binaries += crypto_testdriver packet_id_testdriver auth_token_testdriver ncp_testdriver misc_testdriver \
	pkt_testdriver ssl_testdriver user_pass_testdriver push_update_msg_testdriver

if HAVE_LD_WRAP_SUPPORT
if !WIN32
test_binaries += tls_crypt_testdriver
endif
endif

test_binaries += provider_testdriver

if WIN32
test_binaries += cryptoapi_testdriver
LDADD = -lws2_32
endif

if HAVE_SOFTHSM2
if !WIN32
test_binaries += pkcs11_testdriver
endif
endif

if !CROSS_COMPILING
TESTS = $(test_binaries)
endif
check_PROGRAMS = $(test_binaries)

if HAVE_SITNL
check_PROGRAMS += networking_testdriver
endif

argv_testdriver_CFLAGS  = -I$(top_srcdir)/src/openvpn -I$(top_srcdir)/src/compat @TEST_CFLAGS@
argv_testdriver_LDFLAGS = @TEST_LDFLAGS@ -L$(top_srcdir)/src/openvpn -Wl,--wrap=parse_line
argv_testdriver_SOURCES = test_argv.c \
	mock_msg.c mock_msg.h test_common.h \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/argv.c

buffer_testdriver_CFLAGS  = -I$(top_srcdir)/src/openvpn -I$(top_srcdir)/src/compat @TEST_CFLAGS@
buffer_testdriver_LDFLAGS = @TEST_LDFLAGS@ -L$(top_srcdir)/src/openvpn -Wl,--wrap=parse_line
buffer_testdriver_SOURCES = test_buffer.c \
	mock_msg.c mock_msg.h test_common.h \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/platform.c

crypto_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@
crypto_testdriver_LDFLAGS = @TEST_LDFLAGS@
crypto_testdriver_SOURCES = test_crypto.c \
	mock_msg.c mock_msg.h test_common.h \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/mtu.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/mss.c

ssl_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@
ssl_testdriver_LDFLAGS = @TEST_LDFLAGS@  $(OPTIONAL_CRYPTO_LIBS)
ssl_testdriver_SOURCES = test_ssl.c \
	mock_msg.c mock_msg.h test_common.h \
	mock_management.c \
	mock_ssl_dependencies.c mock_win32_execve.c \
	$(top_srcdir)/src/openvpn/argv.c \
	$(top_srcdir)/src/openvpn/base64.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/compat/compat-strsep.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/cryptoapi.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/env_set.c \
	$(top_srcdir)/src/openvpn/mss.c \
	$(top_srcdir)/src/openvpn/mtu.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/options_util.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/run_command.c \
	$(top_srcdir)/src/openvpn/ssl_openssl.c \
	$(top_srcdir)/src/openvpn/ssl_mbedtls.c \
	$(top_srcdir)/src/openvpn/ssl_util.c \
	$(top_srcdir)/src/openvpn/ssl_verify_mbedtls.c \
	$(top_srcdir)/src/openvpn/ssl_verify_openssl.c \
	$(top_srcdir)/src/openvpn/xkey_helper.c \
	$(top_srcdir)/src/openvpn/xkey_provider.c \
	$(top_srcdir)/src/openvpn/win32-util.c

if WIN32
ssl_testdriver_LDADD =  -lcrypt32 -lncrypt -lfwpuclnt -liphlpapi -lws2_32
endif

packet_id_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@
packet_id_testdriver_LDFLAGS = @TEST_LDFLAGS@
packet_id_testdriver_SOURCES = test_packet_id.c \
	mock_msg.c mock_msg.h test_common.h \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/reliable.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/session_id.c

pkt_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@
pkt_testdriver_LDFLAGS = @TEST_LDFLAGS@
pkt_testdriver_SOURCES = test_pkt.c mock_msg.c mock_msg.h mock_win32_execve.c test_common.h \
	$(top_srcdir)/src/openvpn/argv.c \
	$(top_srcdir)/src/openvpn/base64.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/env_set.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/reliable.c \
	$(top_srcdir)/src/openvpn/run_command.c \
	$(top_srcdir)/src/openvpn/session_id.c \
	$(top_srcdir)/src/openvpn/ssl_pkt.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/tls_crypt.c

if !WIN32
tls_crypt_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@
tls_crypt_testdriver_LDFLAGS = @TEST_LDFLAGS@ \
	-Wl,--wrap=buffer_read_from_file \
	-Wl,--wrap=buffer_write_file \
	-Wl,--wrap=parse_line \
	-Wl,--wrap=rand_bytes
tls_crypt_testdriver_SOURCES = test_tls_crypt.c \
	mock_msg.c mock_msg.h test_common.h \
	mock_win32_execve.c \
	$(top_srcdir)/src/openvpn/argv.c \
	$(top_srcdir)/src/openvpn/base64.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/env_set.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/run_command.c
endif

if HAVE_SITNL
networking_testdriver_CFLAGS = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@ $(OPTIONAL_CRYPTO_CFLAGS)
networking_testdriver_LDFLAGS = @TEST_LDFLAGS@ -L$(top_srcdir)/src/openvpn \
	$(OPTIONAL_CRYPTO_LIBS)
networking_testdriver_SOURCES = test_networking.c mock_msg.c \
	$(top_srcdir)/src/openvpn/networking_sitnl.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c
endif

provider_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@ $(OPTIONAL_CRYPTO_CFLAGS)
provider_testdriver_LDFLAGS = @TEST_LDFLAGS@ \
	$(OPTIONAL_CRYPTO_LIBS)

provider_testdriver_SOURCES = test_provider.c mock_msg.c \
	$(top_srcdir)/src/openvpn/xkey_helper.c \
	$(top_srcdir)/src/openvpn/xkey_provider.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/base64.c \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/platform.c

if WIN32
cryptoapi_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@ $(OPTIONAL_CRYPTO_CFLAGS)
cryptoapi_testdriver_LDFLAGS = @TEST_LDFLAGS@ \
	$(OPTIONAL_CRYPTO_LIBS) -lcrypt32 -lncrypt
cryptoapi_testdriver_SOURCES = test_cryptoapi.c mock_msg.c \
	pkey_test_utils.c cert_data.h \
	$(top_srcdir)/src/openvpn/xkey_helper.c \
	$(top_srcdir)/src/openvpn/xkey_provider.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/base64.c \
	$(top_srcdir)/src/openvpn/platform.c \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/win32-util.c
endif

if HAVE_SOFTHSM2
if !WIN32
pkcs11_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@ $(OPTIONAL_CRYPTO_CFLAGS)
pkcs11_testdriver_LDFLAGS = @TEST_LDFLAGS@ \
	$(OPTIONAL_CRYPTO_LIBS)
pkcs11_testdriver_SOURCES = test_pkcs11.c \
	mock_msg.c test_common.h \
	pkey_test_utils.c cert_data.h mock_get_random.c \
	$(top_srcdir)/src/openvpn/xkey_helper.c \
	$(top_srcdir)/src/openvpn/xkey_provider.c \
	$(top_srcdir)/src/openvpn/argv.c \
	$(top_srcdir)/src/openvpn/env_set.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/run_command.c \
	$(top_srcdir)/src/openvpn/base64.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/pkcs11.c \
	$(top_srcdir)/src/openvpn/pkcs11_openssl.c
endif
endif

auth_token_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@ $(OPTIONAL_CRYPTO_CFLAGS)
auth_token_testdriver_LDFLAGS = @TEST_LDFLAGS@ \
	$(OPTIONAL_CRYPTO_LIBS)

auth_token_testdriver_SOURCES = test_auth_token.c \
	mock_msg.c test_common.h \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/base64.c


user_pass_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@
user_pass_testdriver_LDFLAGS = @TEST_LDFLAGS@

user_pass_testdriver_SOURCES = test_user_pass.c \
	mock_msg.c test_common.h \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/console.c \
	$(top_srcdir)/src/openvpn/env_set.c \
	mock_win32_execve.c \
	$(top_srcdir)/src/openvpn/run_command.c \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/base64.c


ncp_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	@TEST_CFLAGS@ $(OPTIONAL_CRYPTO_CFLAGS)
ncp_testdriver_LDFLAGS = @TEST_LDFLAGS@ \
	$(OPTIONAL_CRYPTO_LIBS)

ncp_testdriver_SOURCES = test_ncp.c \
	mock_msg.c test_common.h \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/crypto.c \
	$(top_srcdir)/src/openvpn/crypto_epoch.c \
	$(top_srcdir)/src/openvpn/crypto_mbedtls.c \
	$(top_srcdir)/src/openvpn/crypto_openssl.c \
	$(top_srcdir)/src/openvpn/otime.c \
	$(top_srcdir)/src/openvpn/packet_id.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/compat/compat-strsep.c \
	$(top_srcdir)/src/openvpn/ssl_util.c

misc_testdriver_CFLAGS  = \
	-I$(top_srcdir)/include -I$(top_srcdir)/src/compat -I$(top_srcdir)/src/openvpn \
	-DSOURCEDIR=\"$(top_srcdir)\" @TEST_CFLAGS@

misc_testdriver_LDFLAGS = @TEST_LDFLAGS@

misc_testdriver_SOURCES = test_misc.c \
	mock_msg.c test_common.h  \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/options_util.c \
	$(top_srcdir)/src/openvpn/ssl_util.c \
	$(top_srcdir)/src/openvpn/win32-util.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/list.c

push_update_msg_testdriver_CFLAGS = -I$(top_srcdir)/src/openvpn \
	-I$(top_srcdir)/src/compat \
	-I$(top_srcdir)/tests/unit_tests/openvpn \
	@TEST_CFLAGS@

push_update_msg_testdriver_LDFLAGS = \
	@TEST_LDFLAGS@ \
	-L$(top_srcdir)/src/openvpn

push_update_msg_testdriver_SOURCES = test_push_update_msg.c \
	mock_msg.c \
	mock_get_random.c \
	$(top_srcdir)/src/openvpn/buffer.c \
	$(top_srcdir)/src/openvpn/platform.c \
	$(top_srcdir)/src/openvpn/push_util.c \
	$(top_srcdir)/src/openvpn/options_util.c \
	$(top_srcdir)/src/openvpn/otime.c