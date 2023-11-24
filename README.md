# Notes on Elixir

## Learning Resources
#### Not an endorsement

### Online courses
- [Elixir Lang](https://elixir-lang.org)
- [Elixir School](https://elixirschool.com)
- [Grox.io](https://grox.io)
- [Pragmatic Studio](https://pragmaticstudio.com)
- [Dockyard Academy](https://academy.dockyard.com)

### Video & Screencasts
- [Elixir Casts](https://elixircasts.io)
- [Alchemist Camp](https://alchemist.camp)
- [Elixir for Programmers, 2nd Edition](https://codestool.coding-gnome.com/courses/elixir-for-programmers-2)

### Books
- [Elixir in Action, 3rd Edition, by Sasa Juric](https://www.manning.com/books/elixir-in-action-third-edition)
- [Programming Elixir 1.6, Dave Thomas](https://pragprog.com/titles/elixir16/programming-elixir-1-6/)
- [The Little Elixir \& OTP Guidebook, Benjamin Tan Wei Hao](https://www.manning.com/books/the-little-elixir-and-otp-guidebook)
- [Designing Elixir Systems with OTP, James Edward Gray II and Bruce Tate](https://pragprog.com/titles/jgotp/designing-elixir-systems-with-otp/)
- [Programming Phoenix, Chris McCord, Bruce Tate, and Jose Valim](https://pragprog.com/titles/phoenix14/programming-phoenix-1-4/)
- [THe Phoenix LiveView Cookbook, Chris Gregori](https://www.liveviewcookbook.com/)

## Installation

[Official Installation Guide](https://elixir-lang.org/install.html)

[ASDF Elixir version Management](https://github.com/asdf-vm/asdf)
then in a shell:
- `asdf plugin add erlang`
- `asdf plugin add elixir`
- `asdf list-all erlang`
- `asdf install erlang` <VERSION>, where version matches a recent entry from the list
- `asdf list-all elixir`
- `asdf install elixir <VERSION>`, where version matches a recent entry from the list and is compatible with OTP
- `asdf global erlang <VERSION>` to set a default global version of erlang
- `asdf global elixir <VERSION>` to set a default global version of elixir
- `asdf local erlang <VERSION>` to set a local (folder level) version of erlang
- `asdf local elixir <VERSION>` to set a local (folder level) version of elixir
- `asdf install` to set version referenced in a local `.tools-version` file

## Tools
#### See [Elixir Docs](https://elixir-lang.org/docs.html) for more details

### [Mix](https://hexdocs.pm/mix/1.15.7/Mix.html)
`$mix new <PATH> [--app APP] [--module MODULE] [--sup] [--umbrella]` 
where `<PATH>` specifies the pathname of project. 

This can be as simple as `mix new foo_bar`, in which case mix will create a new subdirectory of the current path with name `foo_bar'.` . This will create subdirectories `lib` and `test`, with files `foo_bar.ex` and `foo_bar_test.exs`.

    foo_bar
    ├── README.md
    ├── lib
    │   └── foo_bar.ex
    ├── mix.exs
    └── test
        ├── foo_bar_test.exs
        └── test_helper.exs

The application name is inferred from the path and must start with a lowercase ASCII letter followed by lowercase ASCII letters, numbers, or underscores.  While application names follow snake_case convention, Elixir module names are aliases, which must be capitalized and written in CamelCase.  That is, while `mix new foo_bar` creates file `foo_bar/lib/foo_bar.ex`, the module name in that file (if not specified) is tranformed by capitalizing the initial letter, capitalizing letters following underscores, and removing underscores:`FooBar`

    defmodule FooBar do
    @moduledoc """
    Documentation for `FooBar`.
    """
   
    @doc """
    Hello world.
   
    ## Examples
   
        iex> FooBar.hello()
        :world
  
    """
      def hello do
        :world
      end
    end

An optional `--app APP` may be provided to specify the OTP name of project.  `mix new foo_bar --app quux` creates a subdirectory of `foo_bar`, but the source file and script are named after `quux`.

    foo_bar
    ├── README.md
    ├── lib
    │   └── quux.ex
    ├── mix.exs
    └── test
        ├── quux_test.exs
        └── test_helper.exs

The optional `--module MODULE` may be used to specify the module name, which must follow module naming conventions.  `mix new foo_bar --module quux_baz` also creates `foo_bar/lib/quux.ex`.

Including both `--app APP` and `--module MODULE` will result in a file  and module named after `MODULE`.

The `--sup` option may be used to generate an OTP application skeleton including a supervision tree. `mix new foo_bar --sup` generates:

    foo_bar
    ├── README.md
    ├── lib
    │   ├── foo_bar
    │   │   └── application.ex
    │   └── foo_bar.ex
    ├── mix.exs
    └── test
        ├── foo_bar_test.exs
        └── test_helper.exs

Finally, `--umbrella` may be used to generate an umbrella project.  `mix new foo_bar --umbrella` generates

    foo_bar
    ├── README.md
    ├── apps
    ├── config
    │   └── config.exs
    └── mix.exs

Sub-applications may be created under the `apps` subdirectory.
