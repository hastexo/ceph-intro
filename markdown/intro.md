<!-- .slide: data-background="black" -->
## Have Data, Want Scale
# Indefinitely
Exploring Ceph

Florian Haas, [@hastexo](https://twitter.com/hastexo)
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
cooking knife. Strangely enough, though, we seem to be relatively indifferent
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

And unsurprisingly, IT is much the same way. What we're proud
of, what we like to show off, are, say cool visualization libraries...

Source: https://flic.kr/p/79R15s


<!-- .slide: data-background="white" -->
<iframe class="stretch" src="http://bl.ocks.org/kerryrodden/raw/7090426/" scrolling="no"></iframe>
Note: or social networks, or maybe


<!-- .slide: data-background="images/cern-openstack.png" data-background-size="contain" -->
Note: fancy distributed systems solving the mysteries of the
universe.

Source: [CERN](http://www.cern.ch), Belmiro Moreira


<!-- .slide: data-background="https://farm3.staticflickr.com/2607/3868876430_c02559b34e_o_d.jpg" data-background-size="cover" -->
Note: Storage systems, in contrast ...

Source: https://flic.kr/p/6TT1b3


<!-- .slide: data-background="https://farm4.staticflickr.com/3817/12436753284_6f866360c4_k_d.jpg" data-background-size="cover" -->
Note: ... well, people usually find them somewhat boring.

Source: https://flic.kr/p/jWZBsL


<!-- .slide: data-background="https://farm4.staticflickr.com/3506/3694634775_47e9c332e1_o_d.jpg" data-background-size="cover" -->
Note: Yet what's crucially important, what determines whether these
systems are actually useful or whether they are meaningless shells, is
data. And it's how we store that data that makes a huge difference to
the success of those systems.

Source: https://flic.kr/p/6CtYcz


<!-- .slide: data-background="https://farm1.staticflickr.com/59/213521842_29b89f0c50_o_d.jpg" data-background-size="cover" -->
Note: Now in recent history, in the last 10-15 years, we've seen a
revolution sweep away all of IT,...

Source: https://flic.kr/p/jSmB5


<!-- .slide: data-background="http://upload.wikimedia.org/wikipedia/commons/4/4e/Open_Source_Initiative_keyhole.svg" data-background-size="contain" -->
Note:  ... and that revolution is called open source...

Source: http://commons.wikimedia.org/wiki/File:Open_Source_Initiative_keyhole.svg


<!-- .slide: data-background="http://upload.wikimedia.org/wikipedia/en/2/22/Heckert_GNU_white.svg" data-background-size="contain" -->
Note: ...or free software, depending on your personal conviction.

Source: http://en.wikipedia.org/wiki/File:Heckert_GNU_white.svg


<!-- .slide: data-background="https://farm3.staticflickr.com/2607/3868876430_c02559b34e_o_d.jpg" data-background-size="cover" -->
Note: But strangely, the storage industry had maintained a strange
kind of immunity against that revolution. While vendors adopted Linux
as a platform they would support, storage systems were still rife with
vendor lock-in. Vendors would essentially sell you overpriced
refrigerators, and if you so much as wanted to make one refrigerator
talk to another,...

Source: https://flic.kr/p/6TT1b3


<!-- .slide: data-background="https://farm4.staticflickr.com/3777/8847016207_374c5b450e_k_d.jpg" data-background-size="cover" -->
Note: ... tech support and sales reps would laugh at you.  In fact,
they'd even laugh at you if you wanted to kick out the...

Source: https://flic.kr/p/etMgGc


<!-- .slide: data-background="https://farm9.staticflickr.com/8198/8183845721_16efcd1ed4_k_d.jpg" data-background-size="cover" -->
Note: ... fibre channel switch vendor **they** preferred for one that
**you** wanted.

Source: https://flic.kr/p/dtbmdi


<!-- .slide: data-background-image="images/ceph-logo.svg" data-background-color="white" data-background-size="contain" -->
Note: And then came Ceph.

Ceph is a distributed storage system designed to provide block,
file and object storage on a software-defined platform running on
commodity hardware, providing automatic scale-out and high
availability on a Petabyte scale using open replication protocols, all
under a free software license.


<!-- .slide: data-background="images/bingo.png" data-background-size="contain" -->
Note: Too many buzzwords? Thought so. So let's dissect what Ceph is
about, where it came from, and how it's significant and useful. I can
speak my mind freely here, because I run an independent company that
-- while we do work with Ceph very frequently -- is not affiliated
with any business entity that is related to Ceph.


# Lustre
# - suck
--------
# = Ceph

Note: The **original** motivation behind Ceph -- back in 2005 -- was
to provide a distributed filesystem, akin to the then-popular Lustre
filesystem, but without its shortcomings. In short, it was meant to be
"Lustre without the suck".


<!-- .slide: data-background="https://farm2.staticflickr.com/1264/1425884952_70a8ba747e_o_d.jpg" data-background-size="cover" -->
Note: It originally came out of a research project (and PhD thesis) at
the University of California, Santa Cruz (UCSC). The doctoral
candidate was Sage Weil.


<!-- .slide: data-background-color="white" data-background-image="images/object-storage.svg" data-background-size="contain" -->
Note: At the core of Ceph lies the notion of a low-level **object**. And
object is a chunk of data, of arbitrary size with an arbitrary number
of key-value attributes attached to it.


## Reliable
## Autonomic
## Distributed
## Object
## Store
---------
# RADOS
Note: collectively, the distributed object store that Ceph provides is
referred to as RADOS.


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


## librados
## libradospp
## python-ceph
## phprados
Note: Ceph provides a set of CRUSH-aware libraries, which can be used
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
