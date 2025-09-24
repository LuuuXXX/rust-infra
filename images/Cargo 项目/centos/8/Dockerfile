FROM centos:8

# Mirror Repo for amd64
RUN cp -a /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
COPY ./CentOS-8-anon.repo /etc/yum.repos.d/CentOS-Base.repo
RUN yum clean all && yum makecache

# Mirror Repo for arm64
# RUN cp /etc/yum.repos.d/CentOS-*.repo /etc/yum.repos.d/CentOS-*.repo.bak \
# && sed -i 's|^mirrorlist=|#mirrorlist=|g' /etc/yum.repos.d/CentOS-*.repo \
# && sed -i 's|^#baseurl=http://mirror.centos.org/altarch/|baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos-altarch/|g' /etc/yum.repos.d/CentOS-*.repo \
# && sed -i 's|^#baseurl=http://mirror.centos.org/$contentdir/|baseurl=https://mirrors.tuna.tsinghua.edu.cn/centos-altarch/|g' /etc/yum.repos.d/CentOS-*.repo \
# RUN yum clean all && yum makecache

# Install Rust
ENV RUSTUP_DIST_SERVER="https://mirror.xuanwu.openatom.cn"
ENV RUSTUP_UPDATE_ROOT="https://mirror.xuanwu.openatom.cn/rustup"
RUN curl --proto '=https' --tlsv1.2 -sSf https://mirror.xuanwu.openatom.cn/rustup-init.sh | sh -s -- -y
ENV PATH="$PATH:$HOME/.cargo/bin"

# Replace Crates-io
RUN mkdir -p $HOME/.cargo \
&& echo '[source.crates-io]' > $HOME/.cargo/config.toml  \
&& echo 'replace-with = "xuanwu-sparse"' >> $HOME/.cargo/config.toml \
&& echo '[source.xuanwu]' >> $HOME/.cargo/config.toml \
&& echo 'registry = "https://mirror.xuanwu.openatom.cn/crates.io-index"' >> $HOME/.cargo/config.toml \
&& echo '[source.xuanwu-sparse]' >> $HOME/.cargo/config.toml \
&& echo 'registry = "sparse+https://mirror.xuanwu.openatom.cn/index/"' >> $HOME/.cargo/config.toml \
&& echo '[registries.xuanwu]' >> $HOME/.cargo/config.toml \
&& echo 'index = "https://mirror.xuanwu.openatom.cn/crates.io-index"' >> $HOME/.cargo/config.toml \
&& echo '[net]' >> $HOME/.cargo/config.toml \
&& echo 'git-fetch-with-cli = true' >> $HOME/.cargo/config.toml \
&& echo '[http]' >> $HOME/.cargo/config.toml \
&& echo 'check-revoke = false' >> $HOME/.cargo/config.toml

ENV CARGO_NET_GIT_FETCH_WITH_CLI=true
ENV CARGO_HTTP_CHECK_REVOKE=false
ENV CARGO_HTTP_SSL_VERIFY=false
