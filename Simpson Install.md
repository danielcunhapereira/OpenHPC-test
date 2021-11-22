# SIMPSON NMR SIMULATION SOFTWARE INSTALLATION


#download and extract SIMPSON setup for linux 2.4.1.

    wget https://inano.au.dk/fileadmin/user_upload/Simpson_Setup_Linux_4.2.1.tbz2
    tar -xvf Simpson_Setup_Linux_4.2.1.tbz2

#by default simpson installation will direct the binary installation dir as BINDIR="/usr/local/bin" and Library installation dir as LIBDIR="/usr/share/simpson"

#install SIMPSON

    cd Simpson\ Setup\ Linux\ 4.2.1/
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
    
# 
