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
 

