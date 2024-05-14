# Inkblock Graphics Protocol

This is a proposal for a light-weight, cross-platform graphics library that can be implemented in simple C or reimplemented natively in esentially any language.

The basic idea is quite simple: where text based apps use stdin for character input and stdout to "control the terminal", we can instead use stdin/stdout to implement a basic graphical windowing protocol roughly based on the remote framebuffer protocol.

RFBP (RFC 6143) isn't perfectly suited to this task but in its simplest form at least provides the basics of what we need. The biggest missing pieces are multiple-window support, window operation support (raise, lowering, etc.), alternative events for things like game-pads, and of course sound support.

A comparison to XWindows protocol is obviously necessary. XWindows is actually higher level than what I was imagining. It provides things like sub-windows, drawing primitives, font-handling, pixmaps, etc. On the drawing front, RFBP focuses on a single operation - transferring blocks of pixel data. RFBP uses similar key-events to XWindows (apprently with a few twists outlined in RFC 6143) so code already exists in various RDP clients.

# Architecture

We appear to have roughly two basic choices - multiplex a single "connection" (perhaps simply using stdin and stdout connected to pipes) or somehow establish multiple connections (perhaps by launching a proxy for each windows and simply using pipes).

An interesting reason to use a single connection is because it means we can reuse the graphics client stdin/stdout to communicate with the graphics server. Imagine if the first thing printed to STDOUT was some magic number that said "treat my output as inkblock and begin to send me events". The "full screen" launcher would try to make the client behave like an ordinary windowing app, but if launched from a shell inside of a tool like a code editor, now the code editor can control the layout of windows, embed them into the right places, etc. There is a reason the "sixel" format has become popular again...
