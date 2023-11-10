 1. Linux:
	  1. Provide steps to create a directory inside a directory where the parent directory does not exist.
	  2. How to install a package on a Linux server when there is no internet connection?
	  3. How to access specific folders of Server A from Server B and Server C?
	  4. How to check all the running processes from a server?
	  5. Provide the command to delete all the files older than X days inside a specific directory.
    6. Create a shell script to identify the process ID
		a. script should as a user input for process ID
		b. If the process exists script should print the process ID and exit 
		c. If the process doesn't exist script should print the process doesn't exist and asks for another input

## To create a directory inside a non-existing parent directory
    mkdir -p /path/to/nonexistent/parent/directory/newdirectory

## Using a USB drive or another method, move the package (for example, package.deb) to the server.
    sudo dpkg -i package.deb

# From Server B or C, to copy from Server A to local:
    scp user@serverA:/path/to/source/folder/* /path/to/destination/folder/

# To access Server A directly:
    ssh user@serverA
# Checking all running processes on a server:
    ps aux
# Deleting files older than X days in a specific directory:
    find /path/to/directory -type f -mtime +X -exec rm {} \;
Shell script to identify a process ID:
# Save the following script to a file (e.g., check_process.sh), make it executable (chmod +x check_process.sh), and run it (./check_process.sh):

#!/bin/bash

echo -n "Enter the process ID: "
read input_pid

if ps -p $input_pid > /dev/null; then
    echo "Process ID $input_pid exists."
else
    echo "Process ID $input_pid does not exist."
fi


2. Docker:
	1. What is docker and why do we need it?
	2. Write a docker file for a sample Java/python application.
	3. What is the docker lifecycle?
	4. What is the difference between an image and a container?
	5. How to check docker container logs? Provide the command for the same


 1.Docker is a platform for developing, shipping, and running applications in containers. With the help of containers, developers can bundle a programme together with all of its dependencies into a single,
 standardised unit, guaranteeing consistent performance across a range of contexts. Docker facilitates application deployment and management by offering isolation, scalability, and portability.

# sdsd
   # Use an official OpenJDK runtime as a parent image
FROM openjdk:11-jre-slim AS builder

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Build the Java application
RUN javac Main.java

# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory to /app
WORKDIR /app

# Copy the Java application from the builder stage
COPY --from=builder /app/Main.class /app/Main.class

# Copy any Python files
COPY app.py /app/app.py

# Run the Python application
CMD ["python", "app.py"]



