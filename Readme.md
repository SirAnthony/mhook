Mhook, an API hooking library
======

This is fork of original library ( http://codefromthe70s.org/mhook23.aspx )
with a few little modifications.

Changes
-------

1. CMake build.
2. Maximum hooks number increased.
3. Placing more than 1 hook to allocated memory page. 64KB is too much for
   only one 100-bytes trampoline.
