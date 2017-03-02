FROM openjdk:7-jdk
LABEL maintainer peter.kosztolanyi@gmail.com

ENV TALEND_DOWNLOAD_URL=https://sourceforge.net/projects/talendesb/files/Talend%20Open%20Studio%20for%20ESB/5.6.2/TOS_ESB-20150508_1414-V5.6.2.zip/download
ENV TALEND_LOCAL_STORAGE=talend-release

ENV TALEND_CODEGEN_GIT_REPO=https://github.com/kakwa/talend-codegen.git 
ENV TALEND_DIR=/opt/talend
ENV TALEND_CODEGEN_DIR=/opt/talend-codegen

# Update ubuntu and install required packages
RUN apt-get update && apt-get install -y make ant

# Download Talend
#
#    Talend official packages hosted on Sourceforge and it is slow to download in general
#    Need to find a replacement to build the image faster
#RUN wget --no-check-certificate -O $TALEND_DIR.zip $TALEND_DOWNLOAD_URL && unzip $TALEND_DIR.zip -d $TALEND_DIR

# Copy Talend from local storage
#
#    This is here until a fast server is not available to download Talend packages
COPY $TALEND_LOCAL_STORAGE/TOS_ESB-20150508_1414-V5.6.2.zip /opt
RUN mkdir $TALEND_DIR && unzip /opt/TOS*zip -d /opt/talend

# Compile Command Line Code Generation (job-export) Talend plugin and deploy to Talend plugins dir
RUN git clone $TALEND_CODEGEN_GIT_REPO $TALEND_CODEGEN_DIR && cd $TALEND_CODEGEN_DIR && make && cp jar/talend-codegen*.jar /opt/talend/Studio/plugins

# Create talend-codegen output directory
COPY talend-codegen /opt/talend-codegen/bin/talend-codegen
