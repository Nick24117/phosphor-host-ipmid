AM_DEFAULT_SOURCE_EXT = .cpp
AM_CPPFLAGS = -I$(top_srcdir)
sbin_PROGRAMS = phosphor-softpoweroff

# Using ../ instead of $(top_srcdir) due to automake bug in version 1.15.
#  https://debbugs.gnu.org/cgi/bugreport.cgi?bug=13928
phosphor_softpoweroff_SOURCES = \
                    softoff.cpp \
                    ../timer.cpp   \
                    mainapp.cpp \
                    xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.cpp \
                    ../utils.cpp

BUILT_SOURCES = xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.cpp \
                xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.hpp

nodist_include_HEADERS = xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.hpp
CLEANFILES = xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.cpp \
             xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.hpp

phosphor_softpoweroff_LDFLAGS = $(SYSTEMD_LIBS) \
								$(SDBUSPLUS_LIBS) \
								$(PHOSPHOR_LOGGING_LIBS) \
								$(PHOSPHOR_DBUS_INTERFACES_LIBS)
phosphor_softpoweroff_CXXFLAGS = $(SYSTEMD_CFLAGS) \
								 $(SDBUSPLUS_CFLAGS) \
								 $(PHOSPHOR_LOGGING_CFLAGS) \
								 $(PHOSPHOR_DBUS_INTERFACES_CFLAGS)

xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.cpp: ${top_srcdir}/xyz/openbmc_project/Ipmi/Internal/SoftPowerOff.interface.yaml
	@mkdir -p `dirname $@`
	$(SDBUSPLUSPLUS) -r $(top_srcdir) interface server-cpp xyz.openbmc_project.Ipmi.Internal.SoftPowerOff > $@

xyz/openbmc_project/Ipmi/Internal/SoftPowerOff/server.hpp: ${top_srcdir}/xyz/openbmc_project/Ipmi/Internal/SoftPowerOff.interface.yaml
	@mkdir -p `dirname $@`
	$(SDBUSPLUSPLUS) -r $(top_srcdir) interface server-header xyz.openbmc_project.Ipmi.Internal.SoftPowerOff > $@

SUBDIRS = test
