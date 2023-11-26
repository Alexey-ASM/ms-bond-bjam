# Boost.build jam file to support Microsoft Bond compilation

This source code was adapted from Liping Zhang (zhanglpg at gmail dot com)'s code wich adapted from Rodrigo Pinho Pereira de Souza ( pinhopro at gmail dot com )'s code and is now published under Boost License (as it was).

## Usage:

0. Microsoft Bond requires RapidJSON library.
1. Put ms-bond.jam file to a folder on disk, for example /usr/bjam
2. Modify user-config.jam by adding next text

```
import modules : load ;

alias rapidjson
    : # no sources
    : # no build requirements
    : # no default build
    : <include>/path/to/rapidjson/include     # /path/to/rapidjson folder where the rapidjson library is located
;

load ms-bond : : /usr/bjam ;                  # /usr/bjam folder where the ms-bond.jam file is located

using ms-bond : /usr/local : ;                # /usr/local folder where the gbc compiler is located
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
