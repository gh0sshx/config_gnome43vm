# TOOLS

# Table of Contents
1. [mkt](#mkt)
2. [ExtractPorts](#ExtractPorts)
3. [SECLIST](#SECLIST-example)
4. [python2](#python2)
    1. [Fix pip3](#repair_pip3)
5. [NETEXEC](#NETEXEC)
6. [Searchsploit](#Searchsploit)
7. [Kerbrute](#Kerbrute)
8. [Bloodhound and Neo4j](#Bloodhound_and_Neo4j)
    1. [Neo4j](#Neo4j)
    2. [BloodHound](#BloodHound)
9. [Bloodhound and Neo4j](#Bloodhound_and_Neo4j)
10. [LOCATE](#LOCATE)
11. [GEF_on_GDB](#GEF_on_GDB)
12. [FTP](#FTP)
13. [FORMAT_JSON](#FORMAT_JSON)
14. [SHOWMOUNT](#SHOWMOUNT)
15. [keepass](#keepass)
16. [RLWRAP](#RLWRAP)
17. [CRACKMAPEXEC_(OBSOLETE)](#CRACKMAPEXEC_(OBSOLETE))


## mkt

    nano ~/.zshrc
>
    function mkt(){
        mkdir {nmap,content,scripts,tools,content}
    }

## ExtractPorts

    nano ~/.zshrc
>
    # Used: 
    # nmap -p- --open -T5 -v -n ip -oG allPorts

    # Extract nmap information
    # Run as: 
    # extractPorts allPorts
    function extractPorts(){
    	ports="$(cat $1 | grep -oP '\d{1,5}/open' | awk '{print $1}' FS='/' | xargs | tr ' ' ',')"
    	ip_address="$(cat $1 | grep -oP '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}' | sort -u | head -n 1)"
    	echo -e "\n[*] Extracting information...\n" > extractPorts.tmp
    	echo -e "\t[*] IP Address: $ip_address"  >> extractPorts.tmp
    	echo -e "\t[*] Open ports: $ports\n"  >> extractPorts.tmp
    	echo $ports | tr -d '\n' | xclip -sel clip
    	echo -e "[*] Ports copied to clipboard\n"  >> extractPorts.tmp
    	cat extractPorts.tmp; rm extractPorts.tmp
    }


## SECLIST

    wget -c https://github.com/danielmiessler/SecLists/archive/master.zip -O    SecList.zip \
    && unzip SecList.zip \
    && rm -f SecList.zip
>    
    mv SecLists-master SecLists
>
    sudo mv SecLists /usr/share/

## python2 (only debian12 or parrot6)

>add repo debian 11 or kali(recomended)

> debian

    deb http://deb.debian.org/debian bullseye main contrib non-free
    deb http://deb.debian.org/debian bullseye-updates main contrib non-free
    deb http://deb.debian.org/debian bullseye-backports main contrib non-free
    deb http://security.debian.org/debian-security/ bullseye-security main contrib non-free

> kali

    sudo apt install apt-transport-https
>
    wget -q -O - https://archive.kali.org/archive-key.asc | sudo apt-key add -
>
    deb https://http.kali.org/kali kali-rolling main contrib non-free
>
    sudo apt install python2 python2.7

> pip

    wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
>    
    sudo python2.7 get-pip.py    

> remove kali repo from sources.list

> (python2.7 get-pip.py) <= TESTING

### repair_pip3 

    sudo rm /usr/lib/python3.11/EXTERNALLY-MANAGED


## NETEXEC

> https://www.netexec.wiki/getting-started/installation

    sudo apt install pipx git
>
    pipx ensurepath
>
    pipx install git+https://github.com/Pennyw0rth/NetExec

## Searchsploit

    sudo apt -y install exploitdb

## Kerbrute

> download from https://github.com/ropnop/kerbrute

    sudo mkdir /opt/kerbrute && sudo mv kerbrute_linux_amd64 /opt/kerbrute/kerbrute && chmod +x /opt/kerbrute/kerbrute
>
    sudo ln -s /opt/kerbrute/kerbrute /usr/bin/kerbrute

## Bloodhound_and_Neo4j

### Neo4j

> https://neo4j.com/docs/operations-manual/current/installation/linux/debian/#debian-installation

    wget -O - https://debian.neo4j.com/neotechnology.gpg.key | sudo apt-key add -
    echo 'deb https://debian.neo4j.com stable latest' | sudo tee -a /etc/apt/sources.list.d/neo4j.list
    sudo apt-get update
>
    sudo apt-get install neo4j<version 4>

### BloodHound

> https://github.com/BloodHoundAD/BloodHound

    sudo mv BloodHound-linux-x64 /opt
>
    sudo ln -s /opt/BloodHound-linux-x64/BloodHound /usr/bin/BloodHound

> start 
    
    BloodHound --no-sandbox


## LOCATE

    sudo apt install mlocate
>
    sudo updatedb

## GEF_on_GDB

> https://hugsy.github.io/gef/

    bash -c "$(curl -fsSL https://gef.blah.cat/sh)"
>
    pip3 install ropper

> https://github.com/gatieme/GdbPlugins/blob/master/gef/gef.py, copy and paste in gef.py, section with decorator @register

    @register
    class RopperCommand(GenericCommand):
        """Ropper (http://scoding.de/ropper) plugin"""

        _cmdline_ = "ropper"
        _syntax_  = "{:s} [OPTIONS]".format(_cmdline_)


        def __init__(self):
            super(RopperCommand, self).__init__(complete=gdb.COMPLETE_NONE)
            return

        def pre_load(self):
            try:
                __import__("ropper")
            except ImportError:
                msg = "Missing `ropper` package for Python{0}, install with: `pip{0} install ropper`.".format(PYTHON_MAJOR)
                raise GefMissingDependencyException(msg)
            return


        def do_invoke(self, argv):
            ropper = sys.modules["ropper"]
            argv.append("--file")
            argv.append(get_filepath())
            try:
                ropper.start(argv)
            except SystemExit:
                return



## FTP

    sudo apt install curlftpfs

## FORMAT_JSON

    sudo apt install jq


## SHOWMOUNT

    apt-cache search showmount
>
    sudo apt install nfs-common

## keepass

    sudo apt install keepassxc

## RLWRAP

    sudo apt install rlwrap


## CRACKMAPEXEC_(OBSOLETE)

    sudo python3 -m pip install pipx
>
    pipx ensurepath
>
    pipx install crackmapexec