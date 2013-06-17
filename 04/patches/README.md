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

0004-Fix-menu-with-newer-glut-version.patch
===========================================
Do not update menu in menu callback. This avoids illegal operations since the
menu may still be visible when the callback code runs and causes errors with
newer freeglut versions. The (free)glut [documentation][1] advices:

> Remember that it is illegal to create or destroy menus or change, add, or
> remove menu items while a menu (and any cascaded sub-menus) are in use (that
> is, ``popped up''). Use the menu status callback to know when to avoid menu
> manipulation.

The patch updates the menu in an idle callback and
manages a menu_dirty flag that indicates whether or not the menu requires
updating.
