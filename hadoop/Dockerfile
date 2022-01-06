FROM javabase:latest

EXPOSE 8081
EXPOSE 8080
EXPOSE 8088
EXPOSE 7077
EXPOSE 9870
EXPOSE 4040

RUN useradd -m -s /bin/bash hadoop

WORKDIR /home/hadoop

USER hadoop
RUN  wget https://archive.apache.org/dist/hadoop/core/hadoop-3.2.0/hadoop-3.2.0.tar.gz

RUN tar -zxf hadoop-3.2.0.tar.gz && \
    mv hadoop-3.2.0 hadoop && rm *.gz
	
RUN mkdir -p /home/hadoop/.ssh /home/hadoop/hadoop/logs \
    /home/hadoop/data/nameNode /home/hadoop/data/dataNode \
    /home/hadoop/data/namesecondary /home/hadoop/data/tmp && \
    touch /home/hadoop/hadoop/logs/fairscheduler-statedump.log

# We don't care about the skeleton rc files, so overwrite
COPY config/shellrc /home/hadoop/.bashrc
COPY config/shellrc /home/hadoop/.profile
COPY config/id_rsa* /home/hadoop/.ssh/
COPY config/id_rsa.pub  /home/hadoop/.ssh/authorized_keys
COPY config/workers /home/hadoop/spark/conf/slaves
COPY config/hadoopcmd.sh /home/hadoop/
COPY config/hadoop-env.sh /home/hadoop/

COPY config/core-site.xml config/hdfs-site.xml config/mapred-site.xml \
    config/yarn-site.xml config/workers /home/hadoop/hadoop/etc/hadoop/

USER hadoop
RUN cat /home/hadoop/hadoop-env.sh >> /home/hadoop/hadoop/etc/hadoop/hadoop-env.sh

USER root
RUN chown -R hadoop:hadoop /home/hadoop/.ssh /home/hadoop/.bashrc /home/hadoop/.profile \
    /home/hadoop/data /home/hadoop/hadoop-env.sh
#ENTRYPOINT ["/home/hadoop/hadoopcmd.sh","start"]
CMD service ssh start && sleep infinity
