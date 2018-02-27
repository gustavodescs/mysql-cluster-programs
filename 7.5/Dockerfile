FROM mysql/mysql-cluster:7.5 as mysql

RUN yum install -y wget unzip; yum clean all
RUN cd /usr/bin && wget --no-check-certificate https://nextcloud.labbs.com.br/index.php/s/eRPyJ9WvaeNvdG4/download -O mcm-1.4.5-linux-el7-x86-64bit.rpm
RUN cd /usr/bin && wget --no-check-certificate https://nextcloud.labbs.com.br/index.php/s/pzTqQnFLi2sPCF6/download -O ndb_programs.zip
RUN cd /usr/bin && unzip /usr/bin/ndb_programs.zip
RUN mv /usr/bin/programs/* /usr/bin/ \
    && rmdir /usr/bin/programs \
    && rm /usr/bin/ndb_programs.zip
RUN yum install -y /usr/bin/mcm-1.4.5-linux-el7-x86-64bit.rpm
RUN yum erase -y wget unzip; yum clean all
RUN rm -f /usr/bin/mcm-1.4.5-linux-el7-x86-64bit.rpm

RUN cp /usr/mcm1.4.5/bin/* /usr/bin/
RUN cp -r /usr/mcm1.4.5/lib/* /usr/lib/
RUN cp /usr/mcm1.4.5/libexec/* /usr/libexec/
RUN cp /usr/mcm1.4.5/etc/init.d/* /etc/rc.d/init.d/
RUN cp /usr/mcm1.4.5/etc/mcmd.ini /etc/

FROM scratch

COPY --from=mysql / /

ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 3306 33060 2202 1186
