# KI18N Translation Domain for this library
add_definitions(-DTRANSLATION_DOMAIN=\"kcm_smserver\")

set(kcm_smserver_PART_SRCS kcmsmserver.cpp)

qt5_add_dbus_interface(kcm_smserver_PART_SRCS org.freedesktop.login1.Manager.xml login1_manager)

kconfig_add_kcfg_files(kcm_smserver_PART_SRCS smserversettings.kcfgc GENERATE_MOC)

add_library(kcm_smserver MODULE ${kcm_smserver_PART_SRCS})

target_link_libraries(kcm_smserver
    Qt5::Core
    Qt5::DBus
    KF5::QuickAddons
    KF5::I18n
    KF5::ConfigCore
    KF5::KCMUtils
    PW::KWorkspace)

kcoreaddons_desktop_to_json(kcm_smserver "package/metadata.desktop" SERVICE_TYPES kcmodule.desktop)

add_subdirectory(kconf_update)

########### install files ###############

install(TARGETS kcm_smserver DESTINATION ${KDE_INSTALL_PLUGINDIR}/kcms)
install(FILES package/metadata.desktop RENAME kcm_smserver.desktop DESTINATION ${KDE_INSTALL_KSERVICES5DIR})
kpackage_install_package(package kcm_smserver kcms)

