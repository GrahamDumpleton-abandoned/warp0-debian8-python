FROM grahamdumpleton/warp0-base-debian8

MAINTAINER Graham Dumpleton <Graham.Dumpleton@gmail.com>

ENV PYTHON_VERSION=2.7.11 \
    MOD_WSGI_VERSION=4.4.21 \
    WARPDRIVE_VERSION=0.1.0

RUN curl -SL -o /tmp/warpdrive.tar.gz https://codeload.github.com/GrahamDumpleton/warpdrive-python/tar.gz/$WARPDRIVE_VERSION \
    && tar -xC /usr/local --strip-components=1 --exclude README.md -f /tmp/warpdrive.tar.gz \
    && rm -f /tmp/warpdrive.tar.gz 

ENV PATH=/usr/local/warpdrive/bin:$PATH

RUN warpdrive-init

ENV PYTHONHASHSEED=random PATH=/usr/local/python/bin:$PATH

LABEL io.k8s.description="S2I builder for Python web applications." \
      io.k8s.display-name="Python 2.7 (Warp Drive)" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,python,python27,warpdrive,warpdrive-python27" \
      io.openshift.s2i.scripts-url="image:///usr/local/s2i/bin"

ENV STI_SCRIPTS_PATH=/usr/local/s2i/bin

WORKDIR /app

USER 1001

EXPOSE 8080

ENTRYPOINT [ "warpdrive-exec" ]
CMD [ "warpdrive-start" ]
