# warp0-debian8-python

This project contains Docker images for building and deploying Python web
applications based around the [warpdrive](https://github.com/GrahamDumpleton/warpdrive-python)
project.

The ``warp0`` designation indicates this variant is for development and
testing only and should not be used for production. Versions suitable for
production usage will be designated with name ``warpX``, where ``X`` tracks
the major version of ``warpdrive``.

Pre-built versions of the Docker images can be found on Docker Hub as:

  * [grahamdumpleton/warp0-debian8-python27](https://hub.docker.com/r/grahamdumpleton/warp0-debian8-python27/)
  * [grahamdumpleton/warp0-debian8-python35](https://hub.docker.com/r/grahamdumpleton/warp0-debian8-python35/)

The Docker images have been enabled for use with [Source to Image](https://github.com/openshift/source-to-image)
(S2I) and can be used with OpenShift.

Image stream object definitions for OpenShift to allow the S2I builders to
be used from the OpenShift UI can be found in ``openshift.json``. This
can be loaded into OpenShift using:

```
os create -f openshift.json
```
