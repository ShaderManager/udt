Copyright (c) 2001 - 2011, The Board of Trustees of the University of Illinois.
All Rights Reserved.
Copyright (c) 2011 - 2012, Google, Inc. All Rights Reserved.

UDP-based Data Transfer (UDT) Library - version 4
Author: Yunhong Gu [yunhong.gu @ gmail.com]

UDT version 4 is free software under BSD License. See ./LICENSE.txt.

============================================================================

UDT Website:
http://udt.sf.net
http://sf.net/projects/udt/ 

CONTENT: 
./src:     UDT source code 
./doc:     UDT documentation (HTML)

BUILD:
use CMake to generate build files and make library using your favorite build system

RELEASE NOTES:

version 4.11

mostly bug fixes since last version.

version 4.10

added UDT_SNDDATA and UDT_RCVDATA options
fixed a bug that causes unnecessary connection timeout
improved epoll UDT event handling

version 4.9

asynchronous close
asynchronous connect
some bug fixes, especially on EPOLL
improved cache code
removed unnecessary NAK (reduced loss retransmission)
receiver side error can unblock a blocked sender

version 4.8

fix a bug that may cause seg fault on concurrent close on the same socket
add epoll support
increase the listener's scalability to 100K concurrent connections
fix a bug that may cause accept/select to return positively when an accepted socket is closed immediately after accept returns
fix a bug that may cause connect to fail if the server closes listening socket immediately after accept returns
fix recvfile fstream write status bug (e.g., when disk is full, recvfile should handle properly now)

version 4.7a

fix timeout bug introduced in 4.7
initialize CHandShake

version 4.7

Fix several related bugs that can cause hang/memory leak/segmentation fault during cleanup()