cmake_minimum_required(VERSION 3.16)
project(litedoge-qt)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5 COMPONENTS Core Widgets Network DBus Gui REQUIRED)

set_property(SOURCE /src/ui_interface.h PROPERTY SKIP_AUTOUIC ON)
set_property(SOURCE src/ui_interface.h PROPERTY SKIP_AUTOUIC ON)
set_property(SOURCE ui_interface.h PROPERTY SKIP_AUTOUIC ON)

include_directories(
    ${CMAKE_BINARY_DIR}/lib
    ${CMAKE_BINARY_DIR}/include
)

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

# qt5_wrap_ui(FORMS ${FORMS})



include_directories(src src/json src/qt src/qt/forms)

add_subdirectory(src/leveldb)

add_executable(litedoge-qt ${FORMS} ${RESOURCES} ${SOURCES} )
add_dependencies(litedoge-qt leveldb)


target_link_libraries(litedoge-qt PUBLIC
    Qt5::Core
    Qt5::Widgets
    Qt5::Network
    Qt5::DBus
    Qt5::Gui
    leveldb
)
