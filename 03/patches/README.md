
fix_menu_update.diff
====================

Do not update menu in menu callback. This avoids illegal operations since the
menu may still be visible when the callback code runs. This would lead to
errors with newer freeglut versions. The patch updates the menu in an idle
callback and manages a menu_dirty flag that indicates whether or not the menu
requires updating.

fix_non_virtual_destructor.diff
===============================

Fix a missing virtual destructor in abstract class abstract_scene. Its absence
leads to undefined behaviour since the delete operator is called on polymorph
objects of type abstract_scene. Destructors in subclasses may never be called
without this patch.

guard_msvc_specific_pragmas.diff
================================

Guard some MSVC specific pragmas to avoid warnings when using other compilers
than MSC.

