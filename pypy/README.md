# Supported tags and respective `Dockerfile` links

-	[`2-2.5.1`, `2-2.5`, `2-2`, `2` (*2/Dockerfile*)](https://github.com/docker-library/pypy/blob/22b56eb4d32732147f6ce39745febd074f072ecf/2/Dockerfile)
-	[`2-2.5.1-onbuild`, `2-2.5-onbuild`, `2-2-onbuild`, `2-onbuild` (*2/onbuild/Dockerfile*)](https://github.com/docker-library/pypy/blob/b48e8489ab794a2bacfd396c2f8e1a5b06d6ae48/2/onbuild/Dockerfile)
-	[`2-2.5.1-slim`, `2-2.5-slim`, `2-2-slim`, `2-slim` (*2/slim/Dockerfile*)](https://github.com/docker-library/pypy/blob/22b56eb4d32732147f6ce39745febd074f072ecf/2/slim/Dockerfile)
-	[`3-2.4.0`, `3-2.4`, `3-2`, `3`, `latest` (*3/Dockerfile*)](https://github.com/docker-library/pypy/blob/22b56eb4d32732147f6ce39745febd074f072ecf/3/Dockerfile)
-	[`3-2.4.0-onbuild`, `3-2.4-onbuild`, `3-2-onbuild`, `3-onbuild`, `onbuild` (*3/onbuild/Dockerfile*)](https://github.com/docker-library/pypy/blob/b48e8489ab794a2bacfd396c2f8e1a5b06d6ae48/3/onbuild/Dockerfile)
-	[`3-2.4.0-slim`, `3-2.4-slim`, `3-2-slim`, `3-slim`, `slim` (*3/slim/Dockerfile*)](https://github.com/docker-library/pypy/blob/22b56eb4d32732147f6ce39745febd074f072ecf/3/slim/Dockerfile)

For more information about this image and its history, please see the [relevant manifest file (`library/pypy`)](https://github.com/docker-library/official-images/blob/master/library/pypy) in the [`docker-library/official-images` GitHub repo](https://github.com/docker-library/official-images).

# What is PyPy?

PyPy is a Python interpreter and just-in-time compiler. PyPy focuses on speed, efficiency and compatibility with the original CPython interpreter.

PyPy started out as a Python interpreter written in the Python language itself. Current PyPy versions are translated from RPython to C code and compiled. The PyPy JIT (short for "Just In Time") compiler is capable of turning Python code into machine code at run time.

> [wikipedia.org/wiki/PyPy](https://en.wikipedia.org/wiki/PyPy)

![logo](https://raw.githubusercontent.com/docker-library/docs/master/pypy/logo.png)

# How to use this image

## Create a `Dockerfile` in your Python app project

	FROM pypy:3-onbuild
	CMD [ "pypy3", "./your-daemon-or-script.py" ]

or (if you need to use PyPy 2):

	FROM pypy:2-onbuild
	CMD [ "pypy", "./your-daemon-or-script.py" ]

These images include multiple `ONBUILD` triggers, which should be all you need to bootstrap most applications. The build will `COPY` a `requirements.txt` file,`RUN pip install` on said file, and then copy the current directory into`/usr/src/app`.

You can then build and run the Docker image:

	docker build -t my-python-app .
	docker run -it --rm --name my-running-app my-python-app

## Run a single Python script

For many simple, single file projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a Python script by using the Python Docker image directly:

	docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp pypy:3 pypy3 your-daemon-or-script.py

or (again, if you need to use Python 2):

	docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp pypy:2 pypy your-daemon-or-script.py

# Image Variants

The `pypy` images come in many flavors, each designed for a specific use case.

## `pypy:<version>`

This is the defacto image. If you are unsure about what your needs are, you probably want to use this one. It is designed to be used both as a throw away container (mount your source code and start the container to start your app), as well as the base to build other images off of. This tag is based off of [`buildpack-deps`](https://registry.hub.docker.com/_/buildpack-deps/). `buildpack-deps` is designed for the average user of docker who has many images on their system. It, by design, has a large number of extremely common Debian packages. This reduces the number of packages that images that derive from it need to install, thus reducing the overall size of all images on your system.

## `pypy:onbuild`

This image makes building derivative images easier. For most use cases, creating a `Dockerfile` in the base of your project directory with the line `FROM pypy:onbuild` will be enough to create a stand-alone image for your project.

## `pypy:slim`

This image does not contain the common packages contained in the default tag and only contains the minimal packages needed to run `pypy`. Unless you are working in an environment where *only* the pypy image will be deployed and you have space constraints, we highly recommend using the default image of this repository.

# License

View [license information](https://bitbucket.org/pypy/pypy/src/c3ff0dd6252b6ba0d230f3624dbb4aab8973a1d0/LICENSE?at=default) for software contained in this image.

# Supported Docker versions

This image is officially supported on Docker version 1.6.2.

Support for older versions (down to 1.0) is provided on a best-effort basis.

# User Feedback

## Documentation

Documentation for this image is stored in the [`pypy/` directory](https://github.com/docker-library/docs/tree/master/pypy) of the [`docker-library/docs` GitHub repo](https://github.com/docker-library/docs). Be sure to familiarize yourself with the [repository's `README.md` file](https://github.com/docker-library/docs/blob/master/README.md) before attempting a pull request.

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/docker-library/pypy/issues).

You can also reach many of the official image maintainers via the `#docker-library` IRC channel on [Freenode](https://freenode.net).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue](https://github.com/docker-library/pypy/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.
