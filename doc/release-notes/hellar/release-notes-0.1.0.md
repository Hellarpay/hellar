0.1.0 Release notes
====================


Hellar Core version 0.1.0 is now available from:

  https://hellar.io/downloads

Please report bugs using the issue tracker at github:

  https://github.com/hellarpay/hellar/issues




Warning
------------------

Because release 0.1.0 makes use of headers-first synchronization and
parallel block download (see further), the block files and databases are not
backwards-compatible with pre-0.1 versions of Hellar Core or other software:

* Blocks will be stored on disk out of order (in the order they are
received, really), which makes it incompatible with some tools or
other programs. Reindexing using earlier versions will also not work
anymore as a result of this.

* The block index database will now hold headers for which no block is
stored on disk.
This does not affect wallet forward or backward compatibility.


0.1.0 changelog
----------------

Switched to Bitcoin Core version 0.10 - https://bitcoin.org/en/release/v0.10.0
- Implemented decentralized budget system 
- Removed reference node
- Implemented new decentralized masternode payment consensus system
- Improved speed of DS
- New masternode payment/winners/budgets syncing strategy
- Platform independent masternode ranking system
- Masternode broadcasts, pings and winners now use the inventory system
- Transaction indexing is enabled by default for all clients
- Better implementation of IX block reprocessing to find and remove an invalid block
- IX nearly 100% successful with new implementation
- Lots of UI improvements and fixes including DS progress, wallet repair buttons, UI settings/filters persistence etc


Credits
--------

Thanks to who contributed to this release, at least:

eduffield  
UdjinM6  
Crowning  
moli  
flare  
thelazier  
adios  
poiuty  
scratchy  
moocowmoo  
the-baker  
BrainShutdown  
Lukas_Jackson  
Sub-Ether  
italx  
yidakee  
TanteStefana  
coingun  
tungfa  
MangledBlue  
AjM  
Lariondos  
elbereth  
minersday  
qwizzie  
TaoOfSatoshi  
dark-sailor  
AlexMomo  
snogcel
bertlebbert

As well as everyone that helped translating on [Transifex](https://www.transifex.com/projects/p/hellar/).
