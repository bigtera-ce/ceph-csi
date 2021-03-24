FROM ceph/ceph:v14.2
LABEL maintainers="Ceph-CSI Authors"
LABEL description="Ceph-CSI Plugin"

# To support cross building, do NOT RUN native binaries here.
# If we have to run native binaries, qemu-user-static must be installed on
# build host and mounted to container.

# Removing ceph-iscsi repo to workaround the repo issue while upgrading
#RUN rm -f /etc/yum.repos.d/ceph-iscsi.repo && yum -y update && yum clean all
RUN /bin/ln -sf /usr/lib64/ceph/libceph-common.so.0 /usr/lib64/libceph-common.so.0
COPY ceph-fuse /usr/bin/ceph-fuse
ENV CSIBIN=/usr/local/bin/cephcsi

COPY cephcsi $CSIBIN

ENTRYPOINT ["/usr/local/bin/cephcsi"]
