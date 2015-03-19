+++
date = "2015-03-19T10:07:56-06:00"
draft = true
title = "The Thread Pool Pattern"

+++

## ELI5
Your teacher takes out ten pairs of scissors from the supply closet at the
beginning of arts and crafts time. When any of the children need to use
scissors, they ask the teacher, and the teacher will give them a pair, if one's
available. If all ten pairs of scissors are being used, the teacher will go to
the supply closet and get more. When a child is done with the scissors, they are
given back to the teacher to hold on to for the next child who needs it.

This is the *Thread Pool* pattern. Expensive object creation (going into the
closet to get scissors) is managed by reusing created objects (holding on to a
few pairs at once). A manager object creates a repository, or pool, for a set
number of objects to stay, available for use when something requests it. Once
the requester has used the object, it is 'released' back to the pool manager.
The pool can grow or shrink, based on the demand of the pool's objects.

## Code Sample

**To be provided**

## Explanation

**To be provided**
