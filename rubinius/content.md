# What is Rubinius?

Rubinius (http://www.rubini.us) is an implementation of Ruby designed for
concurrency using native threads to run Ruby code on all the CPU cores.

Ruby is a dynamic, reflective, object-oriented, general-purpose, open-source
programming language. According to its authors, Ruby was influenced by Perl,
Smalltalk, Eiffel, Ada, and Lisp. It supports multiple programming paradigms,
including functional, object-oriented, and imperative. It also has a dynamic
type system and automatic memory management.

> [wikipedia.org/wiki/Ruby_(programming_language)](https://en.wikipedia.org/wiki/Ruby_(programming_language))

Rubinius runs Ruby code fast with a low-pause generational garbage collector and
LLVM-based just-in-time (JIT) native machine code compiler.

Rubinius includes a Ruby parser, bytecode virtual machine, bytecode compiler,
generational garbage collector, and just-in-time (JIT) native machine code
compiler. Rubinius uses native OS threads with no global interpreter lock.
Rubinius also provides C-API compatibility for native C extensions.

The Ruby core library is written almost entirely in Ruby. Rubinius tools, such
as the bytecode compiler and debugger, are also written in Ruby.  Rubinius
provides the same standard libraries as Matz's Ruby implementation (MRI) with
the following exceptions:

* Continuation
* Ripper
* TracePoint
* Tracer

Most popular Ruby applications, like Rails, run on Rubinius.

%%LOGO%% Rubinius

# How to use this image

## Create a `Dockerfile` in your Ruby app project

    FROM rubinius:2.4.0-onbuild
    CMD ["./your-daemon-or-script.rb"]

Put this file in the root of your app, next to the `Gemfile`.

This image includes multiple `ONBUILD` triggers which should be all you need to
bootstrap most applications.  The build will `COPY . /usr/src/app` and `RUN
bundle install`.

You can then build and run the Ruby image:

    docker build -t my-ruby-app .
    docker run -it --name my-running-script my-ruby-app

## Run a single Ruby script

For many simple, single file projects, you may find it inconvenient to write a
complete `Dockerfile`. In such cases, you can run a Ruby script by using the
Ruby Docker image directly:

    docker run -it --rm --name my-running-script -v "$(pwd)":/usr/src/myapp -w /usr/src/myapp rubinius:2.4.0 ruby your-daemon-or-script.rb
