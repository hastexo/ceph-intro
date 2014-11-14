<!-- .slide: data-background-image="images/ceph-logo.svg" data-background-color="white" data-background-size="contain" -->
Note: ... came Ceph.

Ceph is a distributed storage system designed to provide block,
file and object storage on a software-defined platform running on
commodity hardware, providing automatic scale-out and high
availability on a Petabyte scale using open replication protocols, all
under a free software license.

Now clearly, that's way too many ...


<!-- .slide: data-background="images/bingo.png" data-background-size="contain" -->
Note: ... buzzwords to be useful, so let's dissect what Ceph is
about, where it came from, and how it's significant and useful. I can
speak my mind freely here, because I run an independent company that
-- while we do work with Ceph very frequently -- is not affiliated
with any business entity that is related to Ceph.

Now the **original** motivation behind Ceph -- back in 2005 -- was
to provide a distributed filesystem, akin to the then-popular Lustre
filesystem, but without its shortcomings. In short, it was meant to be ...


# Lustre
# - suck
--------
# = Ceph

Note: ... "Lustre without the suck".


<!-- .slide: data-background="https://farm2.staticflickr.com/1264/1425884952_70a8ba747e_o_d.jpg" data-background-size="cover" -->
Note: It originally came out of a research project (and PhD thesis) at
the University of California, Santa Cruz (UCSC). The doctoral
candidate was Sage Weil; the research was partially funded by the US
Department of Energy. Sage continues to serve as Ceph's lead developer
to this day, even though Ceph has grown a massive developer community
in the interim.

At the core of Ceph ...


<!-- .slide: data-background-color="white" data-background-image="images/object-storage.svg" data-background-size="contain" -->
Note: ... lies the notion of a low-level **object**. And
object is a chunk of data, of arbitrary size with an arbitrary number
of key-value attributes attached to it.

And collectively, that object store is known as...


## Reliable
## Autonomic
## Distributed
## Object
## Store
---------
# RADOS
Note: ... RADOS.


<!-- .slide: data-background-color="white" data-background-image="images/object-storage.svg" data-background-size="contain" -->
Note: Crucially, the **operations** that can be performed on any
object in the object store are very simple: they boil down to GET, PUT and DELETE
operations.

Objects do not concern themselves with sector
offsets (like block devices), nor with file metadata like permission
bits or file ownership. Why? Because those interfaces complicate what
Ceph is built to shine at:


# Distribution
# Replication


# Distribution
Note: Let's talk about distribution first. If you want to be able to
scale a datastore to the tune of Petabytes or Exabytes, then vertical
scalability (scale-up) is not an option, you will have to go with
horizontal scalability (scale-out).

However, if you distribute by storing where you wrote something
in a central location, then every lookup for every read and write
needs to go through that central location, which by definition becomes
a single point of failure and a bottleneck. This, incidentally, is
exactly the suck in Lustre that Ceph was designed to fix.

So the only way to build this the right way is to devise an
algorithm where the placement of any object is computed, rather than
looked up, and that algorithm is then known to all components in the
environment (servers and clients alike).


## Controlled
## Replication
## Under
## Scalable
## Hashing
----------
# CRUSH
Note: CRUSH is that algorithm, and it's at the heart of Ceph. Every
Ceph client and server component is aware of CRUSH, and can
computationally derive the location of any object in the system. This
eliminates the need for a central lookup facility and opens the system
for massive scalability.


# Replication
Note: CRUSH includes automatic, synchronous **replication**, where
each object is stored in the cluster not once, but a configurable
number of times, and where these replicas are distributed according to
an operator defined policy, such that the system can, for example,
keep copies of each object in separate failure domains.

Now if you want to use Ceph, as an application developer,...


## librados
## libradospp
## python-ceph
## phprados
Note: ... Ceph provides a set of CRUSH-aware libraries, which can be used
to interact with RADOS directly. This enables application developers
to store data in a reliable, distributed, highly available object
store without having to worry **how** exactly that data is stored.

More importantly though, many of these applications have already
been built, so you can use higher level abstractions on the client
side.


## RADOS
## Block
## Device
----
# RBD
Note: This is a block abstraction layer *on top of* the distributed object
store.


<!-- .slide: data-background-color="white" data-background-image="images/block-storage.svg" data-background-size="contain" -->
Note: This means that while you interact with RBD as if it were a
block device, all I/O to and from that device is translated,
transparently, into I/O operations on RADOS objects -- which means
you get distribution and replication for free. Write a block to the
block device, it becomes one or several RADOS objects,
transparently distributed and replicated across the cluster.


# RADOS Gateway
Note: RADOS Gateway enables ReSTful HTTP/S access to objects in the
store using the S3 or Swift protocol.


<!-- .slide: data-background-color="white" data-background-image="images/restful-object-storage.svg" data-background-size="contain" -->
Note: Again, you interact with a well known client protocol and
transparently, without your intervention, this is automatically
distributed and replicated across the cluster.


# CephFS
Note: CephFS finally is what Lustre always wanted to be: a
horizontally scaleable filesystem with built-in high
availability. Crucially though, CephFS is implemented as a **client**
layer, again on top of RADOS.


<!-- .slide: data-background-color="white" data-background-image="images/file-storage.svg" data-background-size="contain" -->
Note: All it has to do is translate POSIX filesystem access into RADOS
object I/O, and it gets distribution and replication for free.

Ceph is readily available to a multitude of applications today.


# Qemu/KVM
Note: Ceph RBD is directly integrated with Qemu/KVM as a storage
driver, enabling you to run virtual machines directly off Ceph RBD
volumes.


<!-- .slide: data-background-image="images/openstack-logo.svg" data-background-size="contain" -->
Note: As such, it is fully available as persistent and ephemeral block
storage in OpenStack.


# CloudStack
# OpenNebula
# Eucalyptus
Note: Ceph is likewise integrated with, and supported by, other
open-source cloud platforms like Apache CloudStack, OpenNebula or
Eucalyptus.


<iframe class="stretch" src="https://asciinema.org/api/asciicasts/13761?speed=3&size=medium&autoplay=1" id="asciicast-iframe-13761" name="asciicast-iframe-13761" scrolling="yes"></iframe>
Note: Deploying Ceph is not rocket science thanks to the `ceph-deploy`
utility, which in this example allowed us to deploy a simple Ceph
cluster in under 4 minutes. Deployment facilities for Puppet, Chef,
Ansible and SaltStack are readily available. More information is
available at http://ceph.com. So go forth and run it, play with it,
join the mailing lists, get on IRC, find me there.
