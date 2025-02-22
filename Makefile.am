ACLOCAL_AMFLAGS = -I build-aux/m4
EXTRA_DIST = \
	CONTRIBUTING.md \
	COPYING \
	COPYRIGHT \
	ChangeLog.md \
	README.cisco \
	README.md \
	autogen \
	sample-ddclient-wrapper.sh \
	sample-etc_cron.d_ddclient \
	sample-etc_dhclient-exit-hooks \
	sample-etc_dhcpc_dhcpcd-eth0.exe \
	sample-etc_ppp_ip-up.local \
	sample-etc_systemd.service \
	sample-get-ip-from-fritzbox
CLEANFILES =

subst_files = ddclient ddclient.conf
EXTRA_DIST += $(subst_files:=.in)
CLEANFILES += $(subst_files)

$(subst_files): Makefile
	rm -f '$@' '$@'.tmp
	in='$@'.in; \
		test -f "$${in}" || in='$(srcdir)/'$${in}; \
		sed \
			-e 's|@PACKAGE_VERSION[@]|$(PACKAGE_VERSION)|g' \
			-e '1 s|^#\!.*perl$$|#\!$(PERL)|g' \
			-e 's|@localstatedir[@]|$(localstatedir)|g' \
			-e 's|@confdir[@]|$(confdir)|g' \
			-e 's|@runstatedir[@]|$(runstatedir)|g' \
			-e 's|@CURL[@]|$(CURL)|g' \
			"$${in}" >'$@'.tmp && \
		{ ! test -x "$${in}" || chmod +x '$@'.tmp; }
	mv '$@'.tmp '$@'

ddclient: $(srcdir)/ddclient.in
ddclient.conf: $(srcdir)/ddclient.conf.in

bin_SCRIPTS = ddclient

conf_DATA = ddclient.conf

install-data-local:
	$(MKDIR_P) '$(DESTDIR)$(localstatedir)'/cache/ddclient

AM_TESTS_ENVIRONMENT = \
	abs_top_srcdir='$(abs_top_srcdir)'; export abs_top_srcdir;
LOG_DRIVER = env AM_TAP_AWK='$(AWK)' $(SHELL) \
	$(top_srcdir)/build-aux/tap-driver.sh
TEST_EXTENSIONS = .pl
PL_LOG_DRIVER = $(LOG_DRIVER)
PL_LOG_COMPILER = $(PERL)
AM_PL_LOG_FLAGS = -Mstrict -w \
	-I'$(abs_top_builddir)' \
	-I'$(abs_top_srcdir)'/t/lib \
	-MDevel::Autoflush
handwritten_tests = \
	t/builtinfw_query.pl \
	t/check_value.pl \
	t/get_ip_from_if.pl \
	t/geturl_connectivity.pl \
	t/geturl_response.pl \
	t/group_hosts_by.pl \
	t/header_ok.pl \
	t/interval_expired.pl \
	t/is-and-extract-ipv4.pl \
	t/is-and-extract-ipv6.pl \
	t/is-and-extract-ipv6-global.pl \
	t/logmsg.pl \
	t/parse_assignments.pl \
	t/protocol_directnic.pl \
	t/protocol_dnsexit2.pl \
	t/protocol_dyndns2.pl \
	t/read_recap.pl \
	t/skip.pl \
	t/ssl-validate.pl \
	t/update_nics.pl \
	t/use_cmd.pl \
	t/use_web.pl \
	t/variable_defaults.pl \
	t/write_recap.pl
generated_tests = \
	t/version.pl
TESTS = $(handwritten_tests) $(generated_tests)
$(TESTS): ddclient
EXTRA_DIST += $(handwritten_tests) \
	.autom4te.cfg \
	t/lib/Devel/Autoflush.pm \
	t/lib/Test/Builder.pm \
	t/lib/Test/Builder/Formatter.pm \
	t/lib/Test/Builder/IO/Scalar.pm \
	t/lib/Test/Builder/Module.pm \
	t/lib/Test/Builder/Tester.pm \
	t/lib/Test/Builder/Tester/Color.pm \
	t/lib/Test/Builder/TodoDiag.pm \
	t/lib/Test/More.pm \
	t/lib/Test/Simple.pm \
	t/lib/Test/Tester.pm \
	t/lib/Test/Tester/Capture.pm \
	t/lib/Test/Tester/CaptureRunner.pm \
	t/lib/Test/Tester/Delegate.pm \
	t/lib/Test/use/ok.pm \
	t/lib/Test2.pm \
	t/lib/Test2/API.pm \
	t/lib/Test2/API/Breakage.pm \
	t/lib/Test2/API/Context.pm \
	t/lib/Test2/API/Instance.pm \
	t/lib/Test2/API/Stack.pm \
	t/lib/Test2/Event.pm \
	t/lib/Test2/Event/Bail.pm \
	t/lib/Test2/Event/Diag.pm \
	t/lib/Test2/Event/Encoding.pm \
	t/lib/Test2/Event/Exception.pm \
	t/lib/Test2/Event/Fail.pm \
	t/lib/Test2/Event/Generic.pm \
	t/lib/Test2/Event/Note.pm \
	t/lib/Test2/Event/Ok.pm \
	t/lib/Test2/Event/Pass.pm \
	t/lib/Test2/Event/Plan.pm \
	t/lib/Test2/Event/Skip.pm \
	t/lib/Test2/Event/Subtest.pm \
	t/lib/Test2/Event/TAP/Version.pm \
	t/lib/Test2/Event/V2.pm \
	t/lib/Test2/Event/Waiting.pm \
	t/lib/Test2/EventFacet.pm \
	t/lib/Test2/EventFacet/About.pm \
	t/lib/Test2/EventFacet/Amnesty.pm \
	t/lib/Test2/EventFacet/Assert.pm \
	t/lib/Test2/EventFacet/Control.pm \
	t/lib/Test2/EventFacet/Error.pm \
	t/lib/Test2/EventFacet/Hub.pm \
	t/lib/Test2/EventFacet/Info.pm \
	t/lib/Test2/EventFacet/Info/Table.pm \
	t/lib/Test2/EventFacet/Meta.pm \
	t/lib/Test2/EventFacet/Parent.pm \
	t/lib/Test2/EventFacet/Plan.pm \
	t/lib/Test2/EventFacet/Render.pm \
	t/lib/Test2/EventFacet/Trace.pm \
	t/lib/Test2/Formatter.pm \
	t/lib/Test2/Formatter/TAP.pm \
	t/lib/Test2/Hub.pm \
	t/lib/Test2/Hub/Interceptor.pm \
	t/lib/Test2/Hub/Interceptor/Terminator.pm \
	t/lib/Test2/Hub/Subtest.pm \
	t/lib/Test2/IPC.pm \
	t/lib/Test2/IPC/Driver.pm \
	t/lib/Test2/IPC/Driver/Files.pm \
	t/lib/Test2/Tools/Tiny.pm \
	t/lib/Test2/Util.pm \
	t/lib/Test2/Util/ExternalMeta.pm \
	t/lib/Test2/Util/Facets2Legacy.pm \
	t/lib/Test2/Util/HashBase.pm \
	t/lib/Test2/Util/Trace.pm \
	t/lib/ddclient/Test/Fake/HTTPD.pm \
	t/lib/ddclient/Test/Fake/HTTPD/dummy-ca-cert.pem \
	t/lib/ddclient/Test/Fake/HTTPD/dummy-server-cert.pem \
	t/lib/ddclient/Test/Fake/HTTPD/dummy-server-key.pem \
	t/lib/ddclient/Test/Fake/HTTPD/other-ca-cert.pem \
	t/lib/ddclient/t.pm \
	t/lib/ddclient/t/HTTPD.pm \
	t/lib/ddclient/t/Logger.pm \
	t/lib/ddclient/t/ip.pm \
	t/lib/ok.pm
