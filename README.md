# Inkblock Graphics Protocol

This is a proposal for a light-weight, cross-platform graphics library that can be implemented in simple C or reimplemented natively in esentially any language.

The basic idea is quite simple: where text based apps use stdin for character input and stdout to "control the terminal", we can instead use stdin/stdout to implement a basic graphical windowing protocol roughly based on the remote framebuffer protocol.

RFBP (RFC 6143) isn't perfectly suited to this task but in its simplest form at least provides the basics of what we need. The biggest missing pieces are multiple-window support, window operation support (raise, lowering, etc.), alternative events for things like game-pads, and of course sound support.
