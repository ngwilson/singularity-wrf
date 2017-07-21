BootStrap: docker
From: centos
Include: yum

# If you want the updates (available at the bootstrap date) to be installed
# inside the container during the bootstrap instead of the General Availability
# point release (7.x) then uncomment the following line
UpdateURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/updates/$basearch/


%runscript
    echo "This is what happens when you run the container."


%post
    yum -y install gcc gcc-c++ gcc-gfortran
    yum -y install make patch m4 git
    yum -y install file
    yum -y install openssl-devel
    yum -y install libibverbs-devel
    yum -y install tar bzip2 gzip unzip
    yum -y install which time
    yum -y install epel-release
    yum -y install python-pip
    yum -y install Lmod
    yum -y install python-setuptools
    yum -y clean all
    mkdir -p /ichec/home
    mkdir -p /ichec/work
    # install easybuild
    cd /
    wget https://raw.githubusercontent.com/hpcugent/easybuild-framework/develop/easybuild/scripts/bootstrap_eb.py
    PREFIX=/opt/apps/easybuild
    chmod 777 /opt /opt/apps
    useradd easybuild
    mkdir /easybuild
    chown easybuild:easybuild /easybuild
    runuser easybuild -c "python /bootstrap_eb.py $PREFIX"
    chmod 755 /opt /opt/apps
    rm -rf /easybuild /bootstrap_eb.py

%environment
    export MODULEPATH=/opt/apps/easybuild/modules/all:$MODULEPATH
    . /etc/profile
