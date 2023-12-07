# Boost.build jam file to support Microsoft Bond compilation

This source code was adapted from Liping Zhang (zhanglpg at gmail dot com)'s code wich adapted from Rodrigo Pinho Pereira de Souza ( pinhopro at gmail dot com )'s code and is now published under Boost License (as it was).

## Usage:

0. Microsoft Bond requires RapidJSON library.
1. Put ms-bond.jam file to a folder on disk, for example /usr/bjam
2. Modify user-config.jam by adding next text

```
import modules : load ;

load ms-bond : : /usr/bjam ;                  # /usr/bjam folder where the ms-bond.jam file is located

using ms-bond ;
```

3. user-config.jam provide include and link paths to bond files eg

```
project 
   : requirements
	 <toolset>msvc:<linkflags>"/LIBPATH:c:/usr/win-x86_64/lib"
	 <include>"c:/usr/include"
;
```

```	 
using gcc : arm_32 : /usr/arm-gcc :
        <linkflags>"-L$(BOOST_ROOT)/stage/linux-arm_32/lib"
        <linkflags>"-L/usr/local/lib_arm32"
        ;

using gcc : arm_64 : /usr/aarch64-gcc :
        <linkflags>"-L$(BOOST_ROOT)/stage/linux-arm_64/lib"
        <linkflags>"-L/usr/local/lib_aarch64"
        ;

using gcc : x86_64 : gcc :
        <linkflags>"-L$(BOOST_ROOT)/stage/linux-x86_64/lib"
        <linkflags>"-L/usr/local/lib"
        ;
```

4. a. Simple exe

```
exe myexe :
	bondFile.bond
	/ms-bond//ms-bond
;
```

4. b. Multiple bond files

```
exe myexe :
	[ glob *.bond ]
	/ms-bond//ms-bond
;
```

4. c. Library

```
lib mylib :
	[ glob *.bond ]
   	/ms-bond//ms-bond
	:
	<link>static 
;

exe myexe : 
   a.cpp
   b.cpp
   : 
   <library>mylib<link>static
 ;
```

Copyright 2023 Alexey Malyshev (alexey dot malyshev at outlook dot ie)
