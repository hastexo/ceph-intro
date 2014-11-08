<!-- .slide: data-background="black" -->
## Have Data, Want Scale
# Indefinitely
An Introduction to Ceph
Note: Every one of us has certain prized possessions. Something that,
despite us all realizing that the truly important things in life are
immaterial, we all have things that we are proud to own and that we
would have trouble giving up.


<!-- .slide: data-background="https://farm6.staticflickr.com/5476/12593834865_ae920f9b55_k_d.jpg" data-background-size="cover" -->
Note: For most people, those are things like maybe a car.

Source: https://flic.kr/p/kbSGkT


<!-- .slide: data-background="https://lh4.googleusercontent.com/-qKxRCUPE8pA/VArO1dh04QI/AAAAAAAAErg/YZwNe1CJqVc/s0-U-I/P4830300.JPG" data-background-size="cover" -->
Note: For me it happens to be this road bicycle, and for many people
it will be their house, or their stereo system, or maybe their best
cooking knife.


Note: Strangely enough, though, we seem to be relatively indifferent
to the things that are the truly important parts of said prized
possessions.


<!-- .slide: data-background="https://farm4.staticflickr.com/3370/3308974893_dc8dfba391_b_d.jpg" data-background-size="cover" -->
Note: For a car, the most important parts, the things that
truly determine whether the car can be driven in the first place, and
the things that can also use potentially fatal damage upon failure,
are the tires.

Source: https://flic.kr/p/63pmXg


<!-- .slide: data-background="https://farm5.staticflickr.com/4021/4624121049_d78fb53cd0_b_d.jpg" data-background-size="cover" -->
Note: And for a house, the part that determines its stability and its
use for shelter the most is arguably the foundation.

Source: https://flic.kr/p/83BQ5Z


<!-- .slide: data-background="https://farm3.staticflickr.com/2713/4038233322_294014df96_o_d.jpg" data-background-size="cover" -->
Note: However, people seem to be much more keen to show off their
living room or their front porch, or their patio, rather than, say,
the concrete in the foundation, or the rebar in that concrete.

Source: https://flic.kr/p/79R15s


Note: And unsurprisingly, IT is much the same way. What we're proud
off, what we like to show off, are social networks, or mobile apps, or
fancy distributed systems solving the mysteries of the universe.


Note: Yet what's crucially important, what determines whether these
systems are actually useful or whether they are meaningless shells, is
data. And it's how we store that data that makes a huge difference to
the success of those systems.


Note: Now in recent history, in the last 10-15 years, we've seen a
revolution sweep away all of IT, and that revolution is called open
source (or free software, depending on your personal conviction).


Note: But strangely, the storage industry had maintained a strange
kind of immunity against that revolution. While vendors adopted Linux
as a platform they would support, storage systems were still rife with
vendor lock-in. Vendors would essentially sell you overpriced
refrigerators, and if you wanted to make one refrigerator talk to
another, tech support and sales reps would laugh at you. In fact,
they'd even laugh at you if you wanted to kick out the fibre channel
switch vendor **they** preferred for one that **you** wanted.


Note: And then came Ceph.


Note: Ceph is a distributed storage system designed to provide block,
file and object storage on a software-defined platform running on
commodity hardware, providing automatic scale-out and high
availability on a Petabyte scale using open replication protocols, all
under a free software license.


Note: Too many buzzwords? Thought so. So let's take a look at how this
works, and what's so special about it.


# Lustre
# - suck
--------
# = Ceph

Note: The **original** motivation behind Ceph -- back in 2005 -- was
to provide a distributed filesystem, akin to the then-popular Lustre
filesystem, but without its shortcomings. In short, it was meant to be
"Lustre without the suck".


Note: It originally came out of a research project (and PhD thesis) at
the University of California, Santa Cruz (UCSC). The doctoral
candidate was Sage Weil.


Note: At the core of Ceph lies the notion of a low-level
**object**. And object is a chunk of data, of arbitrary size with an
arbitrary number of key-value attributes attached to it.


## Reliable
## Autonomic
## Distributed
## Object
## Store
---------
# RADOS
Note: collectively, the distributed object store that Ceph provides is
referred to as RADOS.


Note: Crucially, the **operations** that can be performed on any
object in the object store are very simple: they boil down to GET, PUT and DELETE
operations.



Note: Importantly, objects do not concern themselves with sector
offsets (like block devices), nor with file metadata like permission
bits or file ownership. Why? Because those interfaces complicate what
Ceph is built to shine at:


Note: Distribution


Note: Replication


Note: Let's talk about distribution first. If you want to be able to
scale a datastore to the tune of Petabytes or Exabytes, then vertical
scalability (scale-up) is not an option, you will have to go with
horizontal scalability (scale-out).


Note: However, if you distribute by storing where you wrote something
in a central location, then every lookup for every read and write
needs to go through that central location, which by definition becomes
a single point of failure and a bottleneck. This, incidentally, is
exactly the suck in Lustre that Ceph was designed to fix.


Note: So the only way to build this the right way is to devise an
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


Note: CRUSH includes automatic, synchronous **replication**, where
each object is stored in the cluster not once, but a configurable
number of times, and where these replicas are distributed according to
an operator defined policy, such that the system can, for example,
keep copies of each object in separate failure domains.


Note: Ceph provides a set of CRUSH-aware libraries, which can be used
to interact with RADOS directly. This enables application developers
to store data in a reliable, distributed, highly available object
store without having to worry **how** exactly that data is stored.


Note: more importantly though, many of these applications have already
been built, so you can use higher level abstractions on the client
side.


## RADOS
## Block
## Device
----
# RBD
Note: This is a block abstraction layer *on top of* the distributed object
store. This means that while you interact with RBD as if it were a
block device, all I/O to and from that device is translated,
transparently, into I/O operations on RADOS objects -- which means
you get distribution and replication for free. Write a block to the
block device, it becomes one or several RADOS objects,
transparently distributed and replicated across the cluster.


# RADOS Gateway
Note: RADOS Gateway enables ReSTful HTTP/S access to objects in the
store using the S3 or Swift protocol. Again, you interact with a well
known client protocol and transparently, without your intervention,
this is automatically distributed and replicated across the cluster.


# CephFS
Note: CephFS finally is what Lustre always wanted to be: a
horizontally scaleable filesystem with built-in high
availability. Crucially though, CephFS is implemented as a **client**
layer, again on top of RADOS. All it has to do is translate POSIX
filesystem access into RADOS object I/O, and it gets distribution and
replication for free.


Note: Ceph is readily available to a multitude of applications today.


# Qemu/KVM
Note: Ceph RBD is directly integrated with Qemu/KVM as a storage
driver, enabling you to run virtual machines directly off Ceph RBD
volumes.


# OpenStack
Note: As such, it is fully available as persistent and ephemeral block
storage in OpenStack.


# CloudStack
# OpenNebula
# Eucalyptus
Note: Ceph is likewise integrated with, and supported by, other
open-source cloud platforms like Apache CloudStack, OpenNebula or
Eucalyptus.


