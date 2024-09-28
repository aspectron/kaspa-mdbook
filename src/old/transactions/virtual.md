# VirtualTransaction

VirtualTransaction is a data structure designed to hold multiple instances of `MutableTransaction`.  This data structure helps create large transactions with an unlimited number of outputs by creating and managing a number of smaller MutableTransactions.  Contained MutableTransactions can be related or unrelated.

### TODO