FROM grahamdumpleton/warp0-debian8-base

MAINTAINER Graham Dumpleton <Graham.Dumpleton@gmail.com>

ENV WARPDRIVE_VERSION=0.14.4 \
    PYTHON_VERSION=2.7.11 \
    MOD_WSGI_VERSION=4.4.22

RUN curl -SL -o /tmp/warpdrive.tar.gz https://codeload.github.com/GrahamDumpleton/warpdrive/tar.gz/$WARPDRIVE_VERSION \
    && tar -xC /usr/local --strip-components=1 -f /tmp/warpdrive.tar.gz warpdrive-$WARPDRIVE_VERSION/warpdrive warpdrive-$WARPDRIVE_VERSION/s2i \
    && rm -f /tmp/warpdrive.tar.gz 

ENV PATH=/usr/local/warpdrive/bin:$PATH

RUN warpdrive init

ENV BASH_ENV=/usr/local/warpdrive/etc/shell-init \
    ENV=/usr/local/warpdrive/etc/shell-init \
    PROMPT_COMMAND=". /usr/local/warpdrive/etc/shell-init" \
    STI_SCRIPTS_PATH=/usr/local/s2i/bin \
    PATH=/usr/local/python/bin:$PATH \
    PYTHONHASHSEED=random

LABEL io.k8s.description="S2I builder for Python web applications." \
      io.k8s.display-name="Python 2.7 (Warp Drive)" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,python,python27,warpdrive,warpdrive-python27" \
      io.openshift.s2i.scripts-url="image:///usr/local/s2i/bin"

WORKDIR /opt/warpdrive

USER 1001

EXPOSE 8080

ENTRYPOINT [ "warpdrive", "exec" ]
CMD [ "warpdrive", "start" ]
