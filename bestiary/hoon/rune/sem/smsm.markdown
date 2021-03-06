---
layout: subpage
category: sem
title: semsem
---

`;;`, `semsem`, `[%smsm p=twig q=twig]` is a synthetic hoon that
types `q` as a fixpoint of `p`.

###Definition###

    ++  twig  
      $%  [%smsm p=twig]
      ==

###Regular form (tall)###

    ;;  p
    q

###Regular form (wide)###

    ;;(p q)

###Expansion###
    
    ++  open
      ^-  twig
      ?-    gen
          [%smsm *]
        :+  %tsgr  [%ktts %v ~ 1]                        ::  =>  v=.
        :+  %tsls  [%ktts %a [%tsgr [%cnzy %v] p.gen]]   ::  =+  a==>(v {p.gen})
        :+  %tsls  [%ktts %b [%tsgr [%cnzy %v] q.gen]]   ::  =+  b==>(v {q.gen})
        :+  %tsls                                        ::  =+  c=(a b)
          [%ktts %c [%cnhp [%cnzy %a] [%cnzy %b] ~]]     ::
        [%wtgr [%dtts [%cnzy %c] [%cnzy %b]] [%cnzy %c]] ::  ?>(=(c b) c)
      ==

###Notes###

`;;` can be read as "make sure `q` is a `p`."  `p` should probably be
a tile, not a twig.

The semantics are the same as the present `hoon.hoon` gate
`hard` - ie, `;;(p q)` is `((hard p) q)`.
