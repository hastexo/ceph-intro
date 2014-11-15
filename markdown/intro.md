<!-- .slide: data-background="black" -->
## Have Data, Want Scale
# Indefinitely
Exploring Ceph

Florian Haas, [@hastexo](https://twitter.com/hastexo)
Note: Every one of us has certain prized possessions. Something that,
despite us all realizing that the truly important things in life are
immaterial, we all have things that we are proud to own and that we
would have trouble giving up.

For most people, those are things like ...


<!-- .slide: data-background="https://farm6.staticflickr.com/5476/12593834865_ae920f9b55_k_d.jpg" data-background-size="cover" -->
Note: ... maybe a fancy car, and for me it happens to be ...

Source: https://flic.kr/p/kbSGkT


<!-- .slide: data-background="https://lh4.googleusercontent.com/-qKxRCUPE8pA/VArO1dh04QI/AAAAAAAAErg/YZwNe1CJqVc/s0-U-I/P4830300.JPG" data-background-size="cover" -->
Note: ... this road bicycle, and for many people
it will be their house, or their stereo system, or maybe their best
cooking knife. Strangely enough, though, we seem to be relatively indifferent
to the things that are the truly important parts of said prized
possessions.

For example, for a car, the most important parts, the things that
truly determine whether the car can be driven in the first place, and
the things that can also use potentially fatal damage upon failure,
are the tires.


<!-- .slide: data-background="https://farm4.staticflickr.com/3370/3308974893_dc8dfba391_b_d.jpg" data-background-size="cover" -->
Note: And yet, people who like cars typically really don't show off
their tires that much.

Source: https://flic.kr/p/63pmXg


<!-- .slide: data-background="https://farm5.staticflickr.com/4021/4624121049_d78fb53cd0_b_d.jpg" data-background-size="cover" -->
Note: And for a house, the part that determines its stability and its
use for shelter the most is arguably the foundation.

However, people seem to be much more keen to show off their ...

Source: https://flic.kr/p/83BQ5Z


<!-- .slide: data-background="https://farm3.staticflickr.com/2713/4038233322_294014df96_o_d.jpg" data-background-size="cover" -->
Note: ... front porch or living room or their patio, rather than, say,
the concrete in the foundation, or the rebar in that concrete.

And unsurprisingly, IT is much the same way. What we're proud
of, what we like to show off, are, say cool visualization libraries ...

Source: https://flic.kr/p/79R15s


<!-- .slide: data-background="white" -->
<iframe class="stretch" src="http://bl.ocks.org/kerryrodden/raw/7090426/" scrolling="no"></iframe>
Note: ... or fancy mobile apps or social networks, or maybe ...


<!-- .slide: data-background="images/cern-openstack.png" data-background-size="contain" -->
Note: ... fancy distributed systems solving the mysteries of the
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

Now in recent history, in the last 10-15 years perhaps, ...

Source: https://flic.kr/p/6CtYcz


<!-- .slide: data-background="https://farm1.staticflickr.com/59/213521842_29b89f0c50_o_d.jpg" data-background-size="cover" -->
Note: ... we've been swept up in a revolution in all of IT,...

Source: https://flic.kr/p/jSmB5


<!-- .slide: data-background="http://upload.wikimedia.org/wikipedia/commons/4/4e/Open_Source_Initiative_keyhole.svg" data-background-size="contain" -->
Note:  ... and that revolution is called open source...

Source: http://commons.wikimedia.org/wiki/File:Open_Source_Initiative_keyhole.svg


<!-- .slide: data-background="http://upload.wikimedia.org/wikipedia/en/2/22/Heckert_GNU_white.svg" data-background-size="contain" -->
Note: ...or free software, depending on your personal conviction.

But strangely...

Source: http://en.wikipedia.org/wiki/File:Heckert_GNU_white.svg


<!-- .slide: data-background="https://farm3.staticflickr.com/2607/3868876430_c02559b34e_o_d.jpg" data-background-size="cover" -->
Note: ... the storage industry had maintained a strange
kind of immunity against that revolution. While vendors adopted Linux
as a platform they would support, storage systems were still rife with
vendor lock-in. Vendors would essentially sell you overpriced
refrigerators, and if you so much as wanted to make one refrigerator
talk to another, then the typical reaction from tech people and sales
people alike would be that ...

Source: https://flic.kr/p/6TT1b3


<!-- .slide: data-background="https://farm4.staticflickr.com/3777/8847016207_374c5b450e_k_d.jpg" data-background-size="cover" -->
Note: ... they'd laugh at you.  In fact,
they'd even laugh at you if you wanted to kick out the...

Source: https://flic.kr/p/etMgGc


<!-- .slide: data-background="https://farm9.staticflickr.com/8198/8183845721_16efcd1ed4_k_d.jpg" data-background-size="cover" -->
Note: ... fibre channel switch vendor **they** preferred for one that
**you** wanted.

And then...

Source: https://flic.kr/p/dtbmdi
