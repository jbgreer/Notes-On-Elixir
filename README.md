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

### [Mix](https://hexdocs.pm/mix/1.15.7/Mix.html) is an extensible build tool for creating, compiling, testing, managing dependencies, etc.

#### Mix New
`$mix new <PATH> [--app APP] [--module MODULE] [--sup] [--umbrella]` 
where `<PATH>` specifies the pathname of project. 

This can be as simple as `mix new foo_bar`, in which case mix will create a new subdirectory of the current path with name `foo_bar`. Under `foo_bar` mix will create subdirectories `lib` and `test`, with files `foo_bar.ex` and `foo_bar_test.exs`.

    foo_bar
    ├── README.md
    ├── lib
    │   └── foo_bar.ex
    ├── mix.exs
    └── test
        ├── foo_bar_test.exs
        └── test_helper.exs

The application name is inferred from the path and must start with a lowercase ASCII letter followed by lowercase ASCII letters, numbers, or underscores.  While application names follow snake_case convention, Elixir module names are aliases, which must be capitalized and written in CamelCase.  That is, while `mix new foo_bar` creates file `foo_bar/lib/foo_bar.ex`, the module name in that file (if not specified) is transformed by capitalizing the initial letter and letters following underscores and removing underscores. Hence, module `FooBar`:

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

The optional `--module MODULE` may be used to specify the module name, which must follow module naming conventions.  `mix new foo_bar --module quux` also creates `foo_bar/lib/quux.ex`.

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

#### mix.exs, used for configuration, dependencies, environments, and versions

As seen above `mix new foo_bar` also creates a file, `mix.exs`

    defmodule FooBar.MixProject do
      use Mix.Project
    
      def project do
        [
          app: :foo_bar,
          version: "0.1.0",
          elixir: "~> 1.15",
          start_permanent: Mix.env() == :prod,
          deps: deps()
        ]
      end
    
      # Run "mix help compile.app" to learn about applications.
      def application do
        [
          extra_applications: [:logger]
        ]
      end
    
      # Run "mix help deps" to learn about dependencies.
      defp deps do
        [
          # {:dep_from_hexpm, "~> 0.3.0"},
          # {:dep_from_git, git: "https://github.com/elixir-lang/my_dep.git", tag: "0.1.0"}
        ]
      end
    end

Note that `mix.exs` includes a concept of environments; `:dev`, `:test` and `:prod` environments are defined by default.
Of these, `:dev` is the default environment, except for when running `mix test`, in which case it is `:test`.
One may change the environment by setting the value of `MIX_ENV`, e.g. `$MIX_ENV=prod mix run`

One may also specify that dependendences are only available for certain environments.

#### mix deps.get
If a `mix.exs` containes dependencies, one can fetch them via `mix deps.get`

#### mix compile

To see documentation, `mix help compile.elixir`

#### mix test runs test for a project

`mix test` starts the current application, loads `test/test_helper.exs` and then requires all files matching the `test/**/*_test.ss` pattery in parallel.

One can execute a particular test by `mix test PATH`, where PATH references a particular test script.

#### mix run

`mix run` starts the current application dependencies and the application itself, ∫compiling beforehand if necessary.

### [iex](https://hexdocs.pm/iex/1.15.7/IEx.html) is the Interactive Elixir shell

Type `iex` at a shell prompt will start an interactive shell into which one may type Elixir expressions.
Note that expressions entered in iex are not compiled.

To get shell history, one can invoke `iex --erl "-kernel shell_history enabled"`"

For an Elixir application, it is particular convenient to use `iex -S mix`, which causes iex to execute the `mix.exs` script.

iex is integrated with `Kernel.dbg/2`, and can pause code execution via `iex --dbg pry`.

When running tests via iex, it may be useful to pass --trace to avoid running into timeouts as `iex -S mix test --trace`

Once iex is started, one may type Ctrl-G to reference the switch command menu, from whence one can start a new shell and switch between shells.

One may connect to a remote shell via `iex --sname foo --remsh bar@HOST`


