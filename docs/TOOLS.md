# TOOLS

**SECLIST**

    wget -c https://github.com/danielmiessler/SecLists/archive/master.zip -O    SecList.zip \
    && unzip SecList.zip \
    && rm -f SecList.zip
>    
    mv SecLists-master SecLists
>
    sudo mv SecLists /usr/share/

**CRACKMAPEXEC (OBSOLETE)**

    sudo python3 -m pip install pipx
>
    pipx ensurepath
>
    pipx install crackmapexec

**LOCATE**

    sudo apt install mlocate
>
    sudo updatedb

**HTML2TEXT**

    sudo apt install html2text

**FTP**

    sudo apt install curlftpfs

**FORMAT JSON**

    sudo apt install jq

**PYTHON 2**

    sudo apt-get install python2 python2.7
>

    wget https://www.python.org/ftp/python/2.7.9/Python-2.7.9.tgz
>
    sudo tar xzf Python-2.7.9.tgz
>
    cd Python-2.7.9
>
    sudo ./configure --enable-optimizations
>
    sudo make altinstall
>
    sudo ln -sfn '/usr/local/bin/python2.7' '/usr/bin/python2'
>
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1

> auto mode

    wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
>    
    sudo python2.7 get-pip.py
>    
    python2.7 get-pip.py

**BATCAT**

    sudo apt install bat

**GEF on GDB**

    wget -O ~/.gdbinit-gef.py -q https://gef.blah.cat/py
>
    echo source ~/.gdbinit-gef.py >> ~/.gdbinit
>
    pip install capstone ropper

> https://github.com/gatieme/GdbPlugins/blob/master/gef/gef.py, copy and paste in gef.py, section with decorator @register

    @register_command # @register
    CLASS ROPPERCOMMAND(GENERICCOMMAND):
    """ROPPER (HTTP://SCODING.DE/ROPPER) PLUGIN"""

    _CMDLINE_ = "ROPPER"
    _SYNTAX_  = "{:S} [OPTIONS]".FORMAT(_CMDLINE_)


    DEF __INIT__(SELF):
        SUPER(ROPPERCOMMAND, SELF).__INIT__(COMPLETE=GDB.COMPLETE_NONE)
        RETURN

    DEF PRE_LOAD(SELF):
        TRY:
            __IMPORT__("ROPPER")
        EXCEPT IMPORTERROR:
            MSG = "MISSING `ROPPER` PACKAGE FOR PYTHON{0}, INSTALL WITH: `PIP{0} INSTALL ROPPER`.".FORMAT(PYTHON_MAJOR)
            RAISE GEFMISSINGDEPENDENCYEXCEPTION(MSG)
        RETURN


    DEF DO_INVOKE(SELF, ARGV):
        ROPPER = SYS.MODULES["ROPPER"]
        ARGV.APPEND("--FILE")
        ARGV.APPEND(GET_FILEPATH())
        TRY:
            ROPPER.START(ARGV)
        EXCEPT SYSTEMEXIT:
            RETURN

**SHOWMOUNT**

    apt-cache search showmount
>
    sudo apt install nfs-common

**keepass**

    sudo apt install keepassxc

**SearchSploit**

    sudo apt update && apt -y install exploitdb

**RLWRAP**

    sudo apt install rlwrap


