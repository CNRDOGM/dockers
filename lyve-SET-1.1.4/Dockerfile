FROM centos:centos7

MAINTAINER Otoniel Maya <otto94@gmail.com>

RUN mkdir /data

RUN yum -y update; yum clean all && yum -y upgrade; yum clean all && \
    yum -y groupinstall "Development Tools" ; yum clean all

RUN yum -y install git wget java zlib-devel which perl-core perl-Archive-Tar perl-Digest-MD5 \
    perl-List-MoreUtils perl-Module-CoreList perl-File-Slurp perl-Test-Simple perl-Net-SSLeay perl-IO-Socket-SS ; yum clean all

RUN curl -L http://cpanmin.us | perl - App::cpanminus && cpanm Bio::Perl && cpanm Bio::FeatureIO && \
              cpanm Statistics::Descriptive && cpanm LWP::Protocol::https && cpanm File::Slurp

RUN cd /opt && wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/LATEST/ncbi-blast-2.7.1+-1.x86_64.rpm && \
    rpm -Uvh ncbi-blast-2.7.1+-1.x86_64.rpm && rm -f ncbi-blast-2.7.1+-1.x86_64.rpm && \
    wget -q https://github.com/lskatz/lyve-SET/archive/v1.1.4g.tar.gz && \
    tar -zxvf v1.1.4g.tar.gz && rm -f v1.1.4g.tar.gz && cd lyve-SET-1.1.4g && \
    make install

RUN cd /opt && wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip && \
    unzip Trimmomatic-0.36.zip && rm Trimmomatic-0.36.zip && chmod +x Trimmomatic-0.36/trimmomatic-0.36.jar && \
    ln -s Trimmomatic-0.36/trimmomatic-0.36.jar trimmomatic

ENV PATH=/opt:/opt/lyve-SET-1.1.4g/scripts:$PATH PERL5LIB=/opt/lyve-SET-1.1.4g/lib:$PERL5LIB

VOLUME /data

WORKDIR /data
