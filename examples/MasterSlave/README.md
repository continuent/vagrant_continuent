# Installation

    $ localhost> cd ~
    $ localhost> git clone git@github.com:continuent/continuent-vagrant.git sor
    $ localhost> cd ~/sor
    $ localhost> git submodule update --init
    $ localhost> cp examples/MasterSlave/default.pp ./manifests
    $ localhost> cp examples/Vagrantfile.3.vbox ./Vagrantfile
    $ localhost> ./launch.sh

# Manual Installation

Follow the steps for installation but remove 'clusterData => $clusterData,' prior to running './launch.sh'. After the boxes are launched, proceed with these steps.
    
    $ localhost> vagrant ssh db1
    $ db1> sudo su - tungsten
    $ db1> cd /opt/continuent/software/tungsten-replicator-2.2.0-292

    $ db1> ./tools/tpm configure defaults \
    --user=tungsten \
    --install-directory=/opt/continuent \
    --replication-user=tungsten \
    --replication-password=secret \
    --replication-port=13306 \
    --start-and-report \
    '--profile-script=~/.bash_profile'

    $ db1> ./tools/tpm configure east \
    --topology=master-slave \
    --master=db1 \
    --slaves=db2,db3

    $ db1> ./tools/tpm install