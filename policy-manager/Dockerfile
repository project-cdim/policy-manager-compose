FROM redhat/ubi9

ARG PYTHON_VER="3.14.6"

RUN dnf update -y && \
    dnf -y install git wget nano openssl-devel bzip2-devel libffi-devel zlib-devel ca-certificates postgresql-devel automake cmake make gcc sqlite-devel python3-devel && \
    dnf clean all

RUN wget -Lk "https://www.python.org/ftp/python/$PYTHON_VER/Python-$PYTHON_VER.tgz" -O /tmp/python.tgz && \
    tar -xzvf /tmp/python.tgz
WORKDIR /Python-$PYTHON_VER
RUN sh -c "./configure" && make -j $(nproc) && make install

WORKDIR /policy-manager

ARG CACHE_BUST=1
COPY policy-manager /policy-manager/policy-manager
RUN echo "Cache busting: $CACHE_BUST" && pip3.14 install /policy-manager/policy-manager && mkdir -p /var/log/cdim && \
    find / -xdev \( -perm -4000 -o -perm 2000 \) -type f -exec chmod a-s {} \; 2>/dev/null || true

CMD ["sh","-c","exec policymanager-server"]
