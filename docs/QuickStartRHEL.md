Quick Start - RHEL, Centos, Oracle Linux
========================================

Prerequisites
-------------

This tutorial will help you install Storm on Red Hat Enterprise Linux (RHEL), 
Centos Linux and Oracle Linux.

Introduction
------------

This tutorial provides instructions to get up and running with Storm quickly and 
easily. The instructions in this tutorial show you how to setup Storm in local 
mode, which is the initial mode you'll want to use for development.

Local mode has two main uses:
- To develop Storm topologies
- To deploy a topology to a cluster

In this tutorial, we'll focus on setting up a Storm development environment which 
will allow you to develop Storm topologies.

Download Storm
--------------

Installing wget may not be required if you already have it installed. However 
running yum here is perfectly safe as it'll either install wget if you don't 
have it installed, or will do nothing if wget is already installed.

We first need to switch to the root account, then we'll install wget.

	su - 
	
    yum install wget
    
    exit

Next, we'll setup a few directories to download and install Storm into. I like to 
keep all packages that are installed in my home directory under a packages directory. 
Then I like to symlink the versioned directories in packages to an unversioned 
directory in ~/bin. This makes it easy to upgrade Storm in a development 
environment, and also makes it trivially simple to switch between various 
versions of Storm.

    mkdir ~/bin

    mkdir -p ~/packages/storm

    cd ~/packages/storm

And now let's download Storm.

    wget https://github.com/downloads/nathanmarz/storm/storm-0.8.1.zip

Install Storm
-------------

    unzip storm-0.8.1.zip

    ln -s ~/packages/storm/storm-0.8.1 ~/bin/storm

Congrats. Storm is now installed.

Run the Storm Starter code
--------------------------

We're now going to download and run the Storm Starter code. Storm Starter is a 
Java project that demonstrates how Storm works, including how to create various 
Spouts and Bolts. The Storm Starter project is a great place to start reading 
Java code on how to implement various features in Storm.

As with wget above, we'll run apt-get to install Git and Maven to ensure that 
all necessary sofware is available for our use.

We first need to switch to the root account, then we'll install git and maven.

	su -
	
    yum install git
    
    exit

Installing Maven is a bit more involved.
   
    mkdir -p ~/packages/maven
    
    cd ~/packages/maven
    
    wget http://apache.mirrors.lucidnetworks.net/maven/maven-2/2.2.1/binaries/apache-maven-2.2.1-bin.tar.gz

    tar xzf apache-maven-2.2.1-bin.tar.gz

    ln -s ~/packages/maven/apache-maven-2.2.1 ~/bin/maven

    vi ~/.bash_profile

Update the PATH to
PATH=$PATH:$HOME/bin:$HOME/bin/maven/bin

    source ~/.bash_profile
    
Check that the path is set correctly.

    echo $PATH
    
    which mvn

    mvn –version

You should see multiple lines of output, including:
*Apache Maven 2.2.1*

We're going to create a storm directory in our home directory, which will be 
where we'll store all of our Storm development code. Please feel free to modify 
the path below if you already have a directory structure that you prefer. For 
example, if you use Eclipse then you will likely want to manage all code 
underneath your default Eclipse workspace.

    mkdir ~/storm

    cd ~/storm

Let's grab the Storm Starter project from GitHub.

    git clone https://github.com/nathanmarz/storm-starter.git

    cd ~/storm/storm-starter

We're now ready to compile and run the Word Count Topology using Maven. You'll 
see a large number of tuples stream past in your terminal (hope you can read fast).

    mvn -f m2-pom.xml compile exec:java -Dexec.classpathScope=compile -Dexec.mainClass=storm.starter.WordCountTopology

As a last step, let's run the Exclamation Topology using Maven.

    mvn -f m2-pom.xml compile exec:java -Dexec.classpathScope=compile -Dexec.mainClass=storm.starter.ExclamationTopology
    