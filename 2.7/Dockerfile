FROM grahamdumpleton/warp0-debian8-base

MAINTAINER Graham Dumpleton <Graham.Dumpleton@gmail.com>

ENV WARPDRIVE_VERSION=0.25.0 \
    PYTHON_VERSION=2.7.12 \
    MOD_WSGI_VERSION=4.5.7

ENV WARPDRIVE_APP_ROOT=/opt/app-root \
    WARPDRIVE_SRC_ROOT=/opt/app-root/src

RUN mkdir -p ${WARPDRIVE_APP_ROOT} \
    && curl -SL -o /tmp/warpdrive.tar.gz https://codeload.github.com/GrahamDumpleton/warpdrive/tar.gz/$WARPDRIVE_VERSION \
    && tar -xC ${WARPDRIVE_APP_ROOT} --strip-components=1 -f /tmp/warpdrive.tar.gz warpdrive-$WARPDRIVE_VERSION/warpdrive warpdrive-$WARPDRIVE_VERSION/s2i \
    && rm -f /tmp/warpdrive.tar.gz 

ENV PATH=${WARPDRIVE_APP_ROOT}/warpdrive/bin:$PATH

RUN warpdrive base debian

ENV HOME=${WARPDRIVE_APP_ROOT} \
    BASH_ENV=${WARPDRIVE_APP_ROOT}/warpdrive/etc/shell-init \
    ENV=${WARPDRIVE_APP_ROOT}/warpdrive/etc/shell-init \
    PROMPT_COMMAND=". ${WARPDRIVE_APP_ROOT}/warpdrive/etc/shell-init" \
    STI_SCRIPTS_PATH=${WARPDRIVE_APP_ROOT}/s2i/bin \
    PATH=/usr/local/python/bin:$PATH \
    PYTHONHASHSEED=random

LABEL io.k8s.description="S2I builder for Python web applications." \
      io.k8s.display-name="Python 2.7 (Warp Drive)" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,python,python27,warpdrive,warpdrive-python27" \
      io.openshift.s2i.scripts-url="image://${WARPDRIVE_APP_ROOT}/s2i/bin"

WORKDIR ${WARPDRIVE_SRC_ROOT}

USER 1001

EXPOSE 8080

ENTRYPOINT [ "warpdrive", "exec" ]
CMD [ "warpdrive", "start" ]
