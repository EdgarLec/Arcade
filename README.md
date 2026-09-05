# Arcade

A game platform in C++ that loads **both its graphics libraries and its games as shared objects at
runtime**. Neither the games nor the graphics backends are linked into the binary: the core knows
only two abstract interfaces, and everything else is a `.so` picked up at startup or swapped while
the program runs.

## Why it is built this way

The point of the project is the boundary. A game must not know what draws it, and a graphics library
must not know what it is drawing. So the core defines:

- `IDisplayModule` — open a window, draw, read input, close.
- `IGameModule` — advance one frame of game state, report the score.

Everything else is loaded with `dlopen`/`dlsym`. You can change the renderer without leaving the
game, and add a new backend by dropping a `.so` into `lib/` — no recompilation of the core.

## Backends and games

| Graphics backends | Games |
|---|---|
| ncurses, SDL2, SFML | Centipede, Snake |


## Build

```bash
make            # core + all modules
```

## Run

```bash
./arcade lib/arcade_ncurses.so
```

Then use the in-game menu to switch graphics library or game without restarting.

## Documentation

Generated with Doxygen from `Arcade.doxy`:

```bash
doxygen Arcade.doxy
```

## Context

Epitech project, written in a team.

