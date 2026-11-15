# ghostty-wired

[Ghostty](https://github.com/ghostty-org/ghostty) with patches for the
[wired](https://github.com/twelvehouse/wired-term) terminal emulator, which uses libghostty-vt
(`zig build -Demit-lib-vt`).

- Base: tag `vt-1.0.1` (libghostty-vt 1.0.1).
- Branch `wired` = the base plus the patches below, one commit each. To move to a newer upstream
  tag, rebase `wired` onto it.

## Patches

All patched code is marked with `wired patch` comments.

- **Ignore DEC mode 12 with a default cursor blink** (`src/terminal/stream_terminal.zig`, `setMode`):
  the Ghostty app ignores mode 12 when `cursor-style-blink` is set (`src/termio/stream_handler.zig`),
  but libghostty's stream handler did not, although the C API exposes
  `GHOSTTY_TERMINAL_OPT_DEFAULT_CURSOR_BLINK`. Without it, a program that resets mode 12 on exit
  (ncurses `cnorm`) stops the cursor blink until the next DECSCUSR.

## License

MIT, as upstream; see `LICENSE`.
