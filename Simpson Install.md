# SIMPSON NMR SIMULATION SOFTWARE INSTALLATION


#download and extract SIMPSON setup for linux 2.4.1.

    wget https://inano.au.dk/fileadmin/user_upload/Simpson_Setup_Linux_4.2.1.tbz2 &&
    tar -xvf Simpson_Setup_Linux_4.2.1.tbz2

#by default simpson installation will direct the binary installation dir as BINDIR="/usr/local/bin" and Library installation dir as LIBDIR="/usr/share/simpson"

#install SIMPSON

    cd Simpson\ Setup\ Linux\ 4.2.1/ &&
    ./install.sh

#Now you will be encoutered with an error related with outdated libraries. Comment the two first lines of simpson file

    cd /usr/local/bin

    vi simpson
    
        #!/bin/sh
        #export TCL_LIBRARY=/usr/share/simpson/tcl8.6
        #export LD_LIBRARY_PATH=/usr/share/simpson
        /usr/share/simpson/simpson4.2.1 "$@"
        
#Now you will be encoutered with an error related with a missing librarie package 'liblapack.so.3'. Run the following lines
    
    yum provides '*/liblapack.so.3*'
    
#Install the match package 

    yum install lapack-3.8.0-8.el8.i686
    
#Yet again, if you try to run simpson test.in you will be faced with another error. This time 'undefined symbol: cblas_zgemv'. This is caused by a missing cblas layer on top of BLAS library. You can check what is you version of ATLAS. Recent versions (CentOS7 and CentOS8) do not contain 'libcblas.so.3'. You can change the current version of ATLAS for an older one which contains 'libcblas.so.3', example - 'atlas-3.8.3-5.1.x86_64'. 

    yum remove atlas
    yum intall ftp://ftp.pbone.net/mirror/ftp5.gwdg.de/pub/opensuse/repositories/home:/strohel/openSUSE_Tumbleweed/x86_64/atlas-3.8.3-5.1.x86_64.rpm
    
#Now you can test your test.in file with simpson. 
    
    cd Simpson\ Setup\ Linux\ 4.2.1/
    simpson test.in

#The run should output a 'test.spe'. Happy simulations!
