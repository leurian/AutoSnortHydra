AutoSnortHydra
==============

Additions to the AutoSnort scripting framework to allow it to scale to multiple IDS sensors

Autosnort ( https://github.com/da667/Autosnort ) is a great series of scripts to automate the process of creating, 
compiling, and implomenting Snort and it's rulesets in a new, clean, standalone computer or VM. 

AutoSnortHydra is a series of scripts and frameworks to automate the process of creating multiple Autosnort machines. 
The intent is to have a single 'Mothership' server who distributes the configuration information that can be used in 
Autosnort.sh to simplify multiple machine rollouts. 

Additionally, ASH will intiate a private tunnel back to the Mothership for management, and receive configuration, updates, 
and distribution of IDS events back to a centralised database. 

Intended Operation:

Once the Mothership is configured, a typical workflow would be:

1. From the mothership, create a keypair for a Sensor, based on it's hostname
2. Copy the standard template, make necessary server specific changes (number of promiscuous NICs, Running Services, 
     IP subnets of interest, Mothership as code source, etc.), create an encrypted identity blob
3. Create a clean computer, VM, etc. 
4. Download https://MotherShip/intiate.tar.gz
5. unpack and run initiate.sh
6. initiate.sh queries for hostname of new server, passphrase to unlock identity blob, get clone AutoSnort 
    and AutoSnortHydra/Sensor
7. Changes are made based on the contents of the identity blob to the scripts and AutoSnort.sh is executed
8. Any necessary changes to the system configuration is made to clean up.

Desired functionality:
    Log Rotate and purge for general sensor health
    Server Health (disk free, Snort statistics including dropped packets) sent to Mothership
    Command and Control - have sensors check in every X mintues for rule updates (rsync?)
    
