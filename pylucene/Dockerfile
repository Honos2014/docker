ARG VERSION=latest
FROM python:$VERSION

# 2019-02-17
# docker run -v /YourCodesTestDir:/usr/src/ --name pylucene -ti pylucene /usr/bin/zsh

RUN apt-get update \
    && apt-get install -y default-jdk ant \
    && apt install vim zsh ranger -y

RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

WORKDIR /usr/src/pylucene
RUN curl https://www.apache.org/dist/lucene/pylucene/pylucene-7.6.0-src.tar.gz \
    | tar -xz --strip-components=1
RUN cd jcc \
    && JCC_JDK=/usr/lib/jvm/default-java python setup.py install
RUN make all install JCC='python -m jcc' ANT=ant PYTHON=python NUM_FILES=8

WORKDIR ..
RUN rm -rf pylucene
