---
layout: subpage
axis: doc-hoon
categories: col rune
sort: 30
title: coltar
---

#[coltar, `:*`, %cltr](#cltr)

##Syntax

`:*`, `coltar`, `[%cltr p=tusk]` is a synthetic hoon that
produces a tuple.

###Definition

    ++  twig  
      $%  [%cltr p=tusk]
      ==
    ++  tusk  (list twig)

###Form

####Tall

    :~  i.p
        i.t.p
        i.t.t.p
    ==

####Wide

    :*(i.p i.t.p i.t.t.p)

####Irregular

    [i.p i.t.p i.t.t.p]

###Expansion
    
    ++  open
      ^-  twig
      ?-    gen
          [%cltr *]
        |-  ^-  twig
        ?~  p.gen
          [%zpzp ~]
        =+  mow=jone(gen i.p.gen)
        ?:  =(mow [i.p.gen ~])
          ?~  t.p.gen
            i.p.gen
          [i.p.gen $(p.gen t.p.gen)]
        $(p.gen (weld mow t.p.gen))
      ==
    ::
    ++  jone
      ^-  (list twig)
      ?:  ?=([%clzz *] gen)
        p.gen
      ?:  ?=([%zpcb * [%clzz *]] gen)
        p.q.gen
      [gen ~]


###Notes

`%cltr` also helps us perform some black magic with string
interpolation by automatically promoting `%clzz` twigs.
Otherwise, `%cltr` would simply expand as

    ++  open
      ^-  twig
      ?-    gen
          [%cltr *]
        |-  ^-  twig
        ?~  p.gen
          [%zpzp ~]
        ?~  t.p.gen  i.p.gen
        [i.p.gen $(gen t.p.gen)]
      ==
