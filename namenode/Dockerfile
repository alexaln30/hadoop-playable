FROM bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8

MAINTAINER Ivan Ermilov <ivan.s.ermilov@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:9870/ || exit 1

ENV HDFS_CONF_dfs_namenode_name_dir=file:///hadoop/dfs/name
RUN mkdir -p /hadoop/dfs/name
VOLUME /hadoop/dfs/name
VOLUME /opt/hadoop3.2.1

#Install Sqoop
RUN apt-get update && apt-get install -y wget && apt-get install -y vim && \
	wget http://archive.apache.org/dist/sqoop/1.4.5/sqoop-1.4.5.bin__hadoop-2.0.4-alpha.tar.gz && \
	wget https://github.com/microsoft/mssql-jdbc/releases/download/v8.2.0/mssql-jdbc-8.2.0.jre8.jar && \
	tar xzf sqoop-1.4.5.bin__hadoop-2.0.4-alpha.tar.gz && \
	mv sqoop-1.4.5.bin__hadoop-2.0.4-alpha /usr/lib/sqoop && \
	mv /usr/lib/sqoop/conf/sqoop-env-template.sh /usr/lib/sqoop/conf/sqoop-env.sh && \
	mv mssql-jdbc-8.2.0.jre8.jar /usr/lib/sqoop/lib && \
	rm sqoop-1.4.5.bin__hadoop-2.0.4-alpha.tar.gz && \
    echo "export SQOOP_HOME=/usr/lib/sqoop"  >> ~/.bashrc && \
    echo "export PATH=$PATH:/usr/lib/sqoop/bin" >> ~/.bashrc && \
    echo "export HADOOP_COMMON_HOME=/opt/hadoop-3.2.1" >> /usr/lib/sqoop/conf/sqoop-env.sh && \
    echo "export HADOOP_MAPRED_HOME=/opt/hadoop-3.2.1" >> /usr/lib/sqoop/conf/sqoop-env.sh && \

#	echo "export HADOOP_COMMON_HOME=/opt/hadoop-3.2.1" >> ~/.bashrc && \
#	echo "export HADOOP_MAPRED_HOME=/opt/hadoop-3.2.1" >> ~/.bashrc && \
#	apt-get --purge remove -y wget && \
	apt-get clean

ADD run.sh /run.sh
RUN chmod a+x /run.sh

EXPOSE 9870

CMD ["/run.sh"]
