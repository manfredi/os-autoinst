# SPDX-License-Identifier: MIT
#!BuildTag: os-autoinst_dev:latest opensuse/os-autoinst-dev:latest opensuse/os-autoinst-dev:%PKG_VERSION% opensuse/os-autoinst-dev:%PKG_VERSION%.%RELEASE%
FROM opensuse/tumbleweed

# labelprefix=org.opensuse.os-autoinst-dev
LABEL org.opencontainers.image.title="os-autoinst test container"
LABEL org.opencontainers.image.description="Container for CI testing os-autoinst"
LABEL org.opencontainers.image.version="%PKG_VERSION%.%RELEASE%"
LABEL org.opensuse.reference="registry.opensuse.org/opensuse/os-autoinst-dev:%PKG_VERSION%.%RELEASE%"
LABEL org.openbuildservice.disturl="%DISTURL%"
LABEL org.opencontainers.image.created="%BUILDTIME%"
# endlabelprefix

# Define environment variable
ENV NAME openQA test environment
ENV LANG en_US.UTF-8

# AUTODEPS START
# This part is autogenerated by tools/update-deps from dependencies.yaml
# hadolint ignore=DL3034,DL3037
RUN zypper in -y -C \
       'pkgconfig(fftw3)' \
       'pkgconfig(libpng)' \
       'pkgconfig(opencv)' \
       'pkgconfig(sndfile)' \
       'pkgconfig(theoraenc)' \
       ShellCheck \
       aspell-en \
       aspell-spell \
       cmake \
       cpio \
       ffmpeg \
       file \
       gcc-c++ \
       git-core \
       icewm \
       iproute2 \
       ipxe-bootimgs \
       jq \
       ninja \
       openssh-clients \
       perl-base \
       pkg-config \
       procps \
       python3-Pillow-tk \
       python3-black \
       python3-setuptools \
       python3-yamllint \
       qemu \
       qemu-tools \
       qemu-x86 \
       rsync \
       sed \
       shadow \
       shfmt \
       socat \
       sshpass \
       sudo \
       tesseract-ocr \
       tesseract-ocr-traineddata-english \
       which \
       xorg-x11-Xvnc \
       xterm \
       xterm-console \
       'perl(B::Deparse)' \
       'perl(Benchmark)' \
       'perl(Carp)' \
       'perl(Carp::Always)' \
       'perl(Code::TidyAll)' \
       'perl(Config)' \
       'perl(Cpanel::JSON::XS)' \
       'perl(Crypt::DES)' \
       'perl(Cwd)' \
       'perl(Data::Dumper)' \
       'perl(Devel::Cover)' \
       'perl(Devel::Cover::Report::Codecov)' \
       'perl(Digest::MD5)' \
       'perl(DynaLoader)' \
       'perl(English)' \
       'perl(Errno)' \
       'perl(Exception::Class)' \
       'perl(Exporter)' \
       'perl(ExtUtils::testlib)' \
       'perl(Fcntl)' \
       'perl(Feature::Compat::Try)' \
       'perl(File::Basename)' \
       'perl(File::Find)' \
       'perl(File::Map)' \
       'perl(File::Path)' \
       'perl(File::Temp)' \
       'perl(File::Which)' \
       'perl(File::chdir)' \
       'perl(FindBin)' \
       'perl(IO::Handle)' \
       'perl(IO::Scalar)' \
       'perl(IO::Select)' \
       'perl(IO::Socket)' \
       'perl(IO::Socket::INET)' \
       'perl(IO::Socket::UNIX)' \
       'perl(IPC::Open3)' \
       'perl(IPC::Run::Debug)' \
       'perl(IPC::System::Simple)' \
       'perl(Inline::Lua)' \
       'perl(Inline::Python)' \
       'perl(JSON::Validator)' \
       'perl(List::MoreUtils)' \
       'perl(List::Util)' \
       'perl(Module::CPANfile)' \
       'perl(Mojo::IOLoop::ReadWriteProcess)' \
       'perl(Mojo::JSON)' \
       'perl(Mojo::Log)' \
       'perl(Mojo::URL)' \
       'perl(Mojo::UserAgent)' \
       'perl(Mojolicious)' \
       'perl(Mojolicious::Lite)' \
       'perl(Net::DBus)' \
       'perl(Net::Domain)' \
       'perl(Net::IP)' \
       'perl(Net::SNMP)' \
       'perl(Net::SSH2)' \
       'perl(POSIX)' \
       'perl(Perl::Critic)' \
       'perl(Perl::Critic::Community)' \
       'perl(Perl::Critic::Policy)' \
       'perl(Perl::Critic::Utils)' \
       'perl(Perl::Tidy)' \
       'perl(Pod::Coverage)' \
       'perl(Pod::Html)' \
       'perl(Pod::Spell)' \
       'perl(Scalar::Util)' \
       'perl(Socket)' \
       'perl(Socket::MsgHdr)' \
       'perl(Template::Toolkit)' \
       'perl(Term::ANSIColor)' \
       'perl(Test::CheckGitStatus)' \
       'perl(Test::Mock::Time)' \
       'perl(Test::MockModule)' \
       'perl(Test::MockObject)' \
       'perl(Test::MockRandom)' \
       'perl(Test::Mojo)' \
       'perl(Test::Most)' \
       'perl(Test::Output)' \
       'perl(Test::Pod)' \
       'perl(Test::Strict)' \
       'perl(Test::Warnings)' \
       'perl(Thread::Queue)' \
       'perl(Time::HiRes)' \
       'perl(Time::Moment)' \
       'perl(Time::Seconds)' \
       'perl(XML::LibXML)' \
       'perl(XML::SemanticDiff)' \
       'perl(YAML::PP)' \
       'perl(YAML::XS)' \
       'perl(autodie)' \
       'perl(base)' \
       'perl(constant)' \
       'perl(integer)' \
       'perl(strict)' \
       'perl(version)' \
       'perl(warnings)' \
   && zypper clean
# AUTODEPS END

VOLUME ["/sys/fs/cgroup", "/run"]

CMD ["/sbin/init"]

ENV OPENQA_DIR /opt/openqa
ENV NORMAL_USER squamata

# "nobody" can be used for testing as different user than '$NORMAL_USER'
RUN echo "$NORMAL_USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -r -d /home/$NORMAL_USER -m -g users --uid=1000 $NORMAL_USER
VOLUME [ "/opt/openqa" ]

# explicitly set user/group IDs

RUN mkdir -p /opt/testing_area && \
    chown -R $NORMAL_USER:users /opt/testing_area

ENTRYPOINT ["/bin/bash"]
WORKDIR $OPENQA_DIR
