# Libargs — Myrddin

Commandline argument (flag) parsing library for the Myrddin programming language.

Styled after the Inferno arg.m as per <http://man.cat-v.org/inferno/2/arg>.

The Myrddin programming language: <https://myrlang.org>

## Build

	mbld

## Test

	mbld test

## Install

	mbld install

## Demo

	mbld
	./obj/argsdemo

## Usage

The `args.init()` function must be called before any others.

The `args.argv()` function may be called safely at any time, but is intended to be called after all flags have been parsed.

API reference:

	pkg args =
		// Must be called first ­ initializes the library
		const init     : (args : byte[:][:] → void)

		// Sets the library usage string
		const setusage : (str : byte[:] → void)

		// Emits and exits for usage
		const usage    : (→ void)

		// Emits the next flag character in the flag chain
		const opt      : (→ char)

		// Returns the current argument which must not be nil
		const earg     : (→ byte[:])

		// Returns the argv0 of the input, our program name
		const progname : (→ byte[:])

		// Print remaining arguments
		const argv     : (→ byte[:][:])
	;;


## Example

A more complete example exists in `demo.myr`.

Generic usage of libargs:

	const main = {argv : byte[:][:]

		args.init(argv)

		args.setusage("test [-h] [-n N] name…")

		var c
		while((c = args.opt()) != (0 : char))
			match c
			| 'h':
				std.put("help!\n")
			| 'n':
				std.put("N = {}\n", args.earg())
			| _:
				args.usage()
			;;
		;;

		// Print remaining arguments
		for a : args.argv()
			std.put("→ {}\n", a)
		;;

		…
	}
