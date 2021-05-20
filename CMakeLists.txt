cmake_minimum_required(VERSION 3.16)
project(litedoge-qt)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
# set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
set(BUILD_SHARED_LIBS ON)
# set(CMAKE_EXE_LINKER_FLAGS "-static")

add_compile_definitions(ENABLE_WALLET )
add_compile_definitions(BOOST_THREAD_USE_LIB BOOST_SPIRIT_THREADSAFE BOOST_BIND_GLOBAL_PLACEHOLDERS)



list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}")

find_package(Qt5 COMPONENTS Core Widgets Network DBus Gui REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(Boost 1.67 COMPONENTS system filesystem program_options thread chrono)
find_package(BerkeleyDB REQUIRED) 

set(CMAKE_AUTOUIC_SEARCH_PATHS src/qt/forms)

set(SOURCES 
    src/qt/bitcoin.cpp 
    src/qt/bitcoingui.cpp 
    src/qt/transactiontablemodel.cpp 
    src/qt/addresstablemodel.cpp 
    src/qt/optionsdialog.cpp 
    src/qt/sendcoinsdialog.cpp 
    src/qt/coincontroldialog.cpp 
    src/qt/coincontroltreewidget.cpp 
    src/qt/addressbookpage.cpp 
    src/qt/signverifymessagedialog.cpp 
    src/qt/aboutdialog.cpp 
    src/qt/editaddressdialog.cpp 
    src/qt/bitcoinaddressvalidator.cpp 
    src/alert.cpp 
    src/chainparams.cpp 
    src/version.cpp 
    src/sync.cpp 
    src/txmempool.cpp 
    src/util.cpp 
    src/hash.cpp 
    src/netbase.cpp 
    src/key.cpp 
    src/script.cpp 
    src/core.cpp 
    src/main.cpp 
    src/miner.cpp 
    src/init.cpp 
    src/net.cpp 
    src/checkpoints.cpp 
    src/addrman.cpp 
    src/db.cpp 
    src/walletdb.cpp 
    src/qt/clientmodel.cpp 
    src/qt/guiutil.cpp 
    src/qt/transactionrecord.cpp 
    src/qt/optionsmodel.cpp 
    src/qt/monitoreddatamapper.cpp 
    src/qt/trafficgraphwidget.cpp 
    src/qt/transactiondesc.cpp 
    src/qt/transactiondescdialog.cpp 
    src/qt/bitcoinstrings.cpp 
    src/qt/bitcoinamountfield.cpp 
    src/wallet.cpp 
    src/keystore.cpp 
    src/qt/transactionfilterproxy.cpp 
    src/qt/transactionview.cpp 
    src/qt/walletmodel.cpp 
    src/rpcclient.cpp 
    src/rpcprotocol.cpp 
    src/rpcserver.cpp 
    src/rpcdump.cpp 
    src/rpcmisc.cpp 
    src/rpcnet.cpp 
    src/rpcmining.cpp 
    src/rpcwallet.cpp 
    src/rpcblockchain.cpp 
    src/rpcrawtransaction.cpp 
    src/timedata.cpp 
    src/qt/overviewpage.cpp 
    src/qt/csvmodelwriter.cpp 
    src/crypter.cpp 
    src/qt/sendcoinsentry.cpp 
    src/qt/qvalidatedlineedit.cpp 
    src/qt/bitcoinunits.cpp 
    src/qt/qvaluecombobox.cpp 
    src/qt/askpassphrasedialog.cpp 
    src/protocol.cpp 
    src/qt/notificator.cpp 
    src/qt/paymentserver.cpp 
    src/qt/rpcconsole.cpp 
    src/noui.cpp 
    src/kernel.cpp 
    src/scrypt-arm.S 
    src/scrypt-x86.S 
    src/scrypt-x86_64.S 
    src/scrypt.cpp 
    src/pbkdf2.cpp 
    src/qt/autosaver.cpp
    src/txdb-leveldb.cpp
)

set(FORMS 
    src/qt/forms/coincontroldialog.ui 
    src/qt/forms/sendcoinsdialog.ui 
    src/qt/forms/addressbookpage.ui 
    src/qt/forms/signverifymessagedialog.ui 
    src/qt/forms/aboutdialog.ui 
    src/qt/forms/editaddressdialog.ui 
    src/qt/forms/transactiondescdialog.ui 
    src/qt/forms/overviewpage.ui 
    src/qt/forms/sendcoinsentry.ui 
    src/qt/forms/askpassphrasedialog.ui 
    src/qt/forms/rpcconsole.ui 
    src/qt/forms/optionsdialog.ui
)

set(RESOURCES 
    src/qt/bitcoin.qrc
)


include_directories(src src/json src/qt src/qt/forms ${Boost_INCLUDE_DIRS})
include_directories(src/leveldb/include src/leveldb/helpers)
add_subdirectory(src/leveldb)

add_executable(litedoge-qt ${FORMS} ${RESOURCES} ${SOURCES} )
add_dependencies(litedoge-qt leveldb)


target_link_libraries(litedoge-qt PUBLIC
    Qt5::Core
    Qt5::Widgets
    Qt5::Network
    Qt5::DBus
    Qt5::Gui
    OpenSSL::SSL
    OpenSSL::Crypto
    leveldb
    ${Boost_LIBRARIES}
    Oracle::BerkeleyDB
    # "-static"
)