# Fortran Development Environment

This Directory serves as the source code for a Docker image which is hosted on [Docker Hub](https://hub.docker.com/r/dgisolfi/fortran_dev/) and can be pulled, run and used as a development environment for Fortran. The base image has the GNU Fortran compiler installed, this allows a user to develop programs in an independent environment which avoids complicated downloads and installations on other operating systems. In addition, this keeps your devices hard drive free of compilers that may not be used after the Theory of Programming Languages class is complete.

# Docker Deployment

*Note: If you need assistance with installing Docker, a quick guide can be found [here](https://github.com/dgisolfi/LanguageDevEnvironments)*

To run an instance of the fortran_dev container on your own machine first pull the image by running the following in a terminal:

```bash
docker pull dgisolfi/fortran_dev
```

Next to run an instance of the image as a container run the following:

```bash
docker run -it dgisolfi/fortran_dev bash
```

*Note: If you would like to mount a directory in order to test run the following command instead and replace "/Path/to/Fortran/files" with the path to your files*

```bash
docker run -it -v/Path/to/Fortran/files:/DEV/FortranFiles dgisolfi/fortran_dev bash
```

The result should be command line access as the root user to the now running Docker container. You should be located in the DEV directory within the container. If you chose to Volume mount any files first run `ls` which will list all directories and files, then `cd` into the directory "FortranFiles", anything changed within the mounted directory will be reflected accross both host and container. Due to how volumes work in Docker you have the advantage of the files being shared between the container and your host machine, meaning you may now open the directory up in an IDE and begin to program, any changes in the directory on your host will be reflected in the container.

## Compiling

As an example program, there is an included file "helloworld.f90" located in the "DEV" directory, use this to test the compiler. To compile the file run the following:

```bash
gfortran -o hello helloworld.f90
```

This will create an executable with the name of the program, in this case, "hello" in the directory. Run `./hello` to execute the program.

To run your own programs alter the command to use the following format:

`gfortran -o program_name file_name.f90`

**Note: data inside a Docker container is nonpersistent. Only files that exist inside a volume mounted directory will remain after the container is exited**

With your programs written and mounted you may now use the compiler to test and run them.