My OSX config
=============

I mostly use Linux, but use OSX for work.  My major achievement is setting up a
keyboard shortcut to mute and auto-join hangouts in Chrome, but I've also got a
neat [Hammerspoon](http://www.hammerspoon.org/) config with directional window
switching (basic idea stolen from [FVWM](http://www.fvwm.org/)) and some
automatic window positioning on resolution changes which doesn't quite seem to
work.

Hangouts tools (mute and join)
------------------------------

Both of these use Applescript to send Javascript to Chrome; this Javascript uses
the tooltips on buttons in Hangouts to identify them and click them.

They've worked for me for over a year now with only one change - changing the
target window title from "Google+ Hangouts" to "Google Hangouts".

Mute is fairly straightforward - look for a "Mute microphone" button; if it
doesn't exist, look for an "Unmute microphone" button.  If either exists, send a
mousedown followed by a mouseup a half second later (sending a click event
didn't work for me; this does.)

Join is much more complex; fundamentally, it's hanging up from the existing
hangout if there is one, looking for a current or upcoming meeting, and joining
a default one if there are no meetings.  It can also take a command-line
argument to join a specific hangout, overriding the default behavior.

However, there's a bunch of complexity here, and it doesn't always work.
There's a bug where noon meetings tend to not get detected properly, and
sometimes it seems to not notice meetings and you have to hang up and try again.
Plus, if there's more than one active meeting, it might not join the one you
want.

But for the most part, I've been using it to work remotely, typically on a
hangout all day, switching to meeting-specific ones when needed, and the
"one-button switch" is much nicer than moving the mouse to hangouts, clicking
hangup, waiting for the meetings to load, and clicking the right one.

Hammerspoon
-----------

A former coworker wrote [Slate](https://github.com/jigish/slate) a few years
back, and it was pretty good.  But things have evolved since then; I like
hammerspoon; it's Lua-based, rather than Slate's add-hoc config language, and
just includes everything I want, unlike
[https://github.com/sdegutis/mjolnir](Mjolnir).

Some interesting features I've written:

- Resolution changing: I can press Cmd-Alt-F10 to cycle through resolutions on
  my laptop screen.  Notably, Hammerspoon exposes a relatively low-level API
  that lets you use HiDPI or not; in particular, this lets me use native Retina
  resolution (2880x1800), which I love.  This lets me replace the old
  kind-of-shareware menu button I used to use, and lets me bind it to a
  keystroke instead, which I find more convenient.
- Per-resolution window location saving: This was on of Slate's killer features;
  it let you define layouts and switch to them with a keystroke.  The only
  problem was that finding windows could be a bit tricky, and only windows you
  told it about were saved.  With a full language to write config with, I
  expanded this into "save" and "restore" functions, so I can just save the
  current set of windows (by id, rather than app and title), and restore them
  later.  Plus, since I also use hammerspoon for resolution switching, I can
  autosave when I switch resolutions, and effectively have distinct layouts for
  each resolution.
  Unfortunately, this doesn't seem to fully work, and I don't switch resolutions
  quite often enough to have gotten around to debugging it.
- Manual layouts: Before getting the above working, I implemented some
  hard-coded layouts, just like Slate.
- Directional window switching: One of my favorite features of FVWM, this lets
  me bind HJKL with modifiers to move the focus left/down/up/right.  This is
  surprisingly tricky to do well; the window-choosing algorithm is patterned off
  of FVWM's, but tweaked slightly because, oddly, trying to copy FVWM's source
  resulted in something that really didn't work very well.
- Properly-ordered window hints: Hammerspoon natively supports "window hints",
  placing letters over windows to quickly switch between them.  I much prefer to
  use easy letters rather than mnemonic ones; if I want to switch to a window,
  I'm looking at it anyway, so consistent letters don't matter (not that the
  defaults are consistent anyway...).  So instead, use letters roughly ordered
  by difficulty (IMO - e.g., I prefer e to a; it require motion, but pinkies are
  weak.)
  move 

I also use hammerspoon to add key bindings to my Hangouts scripts described
above.
