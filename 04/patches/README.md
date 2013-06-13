0001-Fix-missing-include.patch
==============================

Fix a missing include in tiny_vec.h that lead to compiler errors.

0002-Guard-MSVC-specific-pragmas.patch
======================================

Guard some MSVC specific pragmas to avoid warnings when using other compilers
than MSC.

0003-Fix-non-virtual-destructor.patch
=====================================

Fix a missing virtual destructor in abstract class abstract_curve. Its absence
leads to undefined behaviour since the delete operator is called on polymorph
objects of type abstract_curve. Destructors in subclasses may never be called
without this patch.
