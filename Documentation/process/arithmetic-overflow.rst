.. _arithmetic_overflow:

Arithmetic Overflow Resolutions for Linux
=========================================

Background
----------

When a calculation’s result exceeds the involved storage ranges, several
strategies can be followed to handle such an overflow (or underflow),
including:

  - Undefined (i.e. pretend it isn’t possible and the result depends on the hardware)
  - Wrap around (this is what 2s-complement representation does by default)
  - Trap (create an exception so the problem can be handled in another way)
  - Saturate (explicitly hold the maximum or minimum representable value)

In the C standard, three basic types can be involved in arithmetic, and each
has a default strategy for solving the overflow problem:

  - Signed overflow is undefined
  - Unsigned overflow explicitly wraps around
  - Pointer overflow is undefined

The Linux kernel uses ``-fno-strict-overflow`` which implies ``-fwrapv`` which
in turn effectively treats signed integer overflow as being consistent with
two's complement. This flag allows for consistency within the codebase about
the expectations of overflowing arithmetic as well as prevents eager compiler
optimizations. Note that :ref:`open-coded intentional arithmetic wrap-around is deprecated <_open_coded_wrap_around>`.

``-fno-strict-overflow`` has no effect on pointer overflow, which is still
undefined. One should not intentionally perform overflowing pointer arithmetic.

From here on, arithmetic overflow concerning signed or unsigned types will be
referred to as "wrap-around" since it is the default strategy for the kernel.

Resolutions
-----------
TODO

  - Sanitizer case lists
  ...

  - Annotations
  ...
