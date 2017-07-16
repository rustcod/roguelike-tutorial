# Introduction

## Welcome!

Hello, and welcome to the Right a [sic] Roguelike in Rust tutorial. This mirrors the popular [roguelike tutorial](http://www.roguebasin.com/index.php?title=Complete_Roguelike_Tutorial,_using_python%2Blibtcod) on Roguebasin, but using the Rust language instead of Python. It also loosely follows a [great Rust port](http://tomassedovic.github.io/roguelike-tutorial/) of that same Python tutorial, but without having to use libtcod, or install SDL2, making it hopefully easier to get going.

## Why Rust?

Rust's unoffical motto is "Safe, Fast, Concurrent, pick three." It is generally billed as a modern replacement for C/C++.

I won't try to do better job at summarizing Rust than the official (and free!) [Rust book's introduction](https://doc.rust-lang.org/book/second-edition/) so take a minute and give that section a read.

Some specific features that make Rust a nice fit for someone making a Roguelike are the compiler, speed of execution, and the stand-out community behind it.

The compiler checks your code up front for silly mistakes, like typos, all the way through complex hard-to-get-right errors like data races from threaded code. While this does mean that learning Rust is more difficult up front, it means that once your code _is_ accepted by the compiler, it generally "Just Works". Coming back to a project, or even a section of code that was written in the past is also easier.

Because your code is checked at compile time, it runs at native (think C/C++) speed. Rust calls this "zero cost abstractions". This means that as your game grows, you're much less likely to hit performance issues. Threading and other forms of parallel coding techniques are also checked at compile time, which means even if you do hit a performance issue, you can spread that work out to take advantage of multiple cores all while the compiler ensures you don't do anything silly.

Finally, there is a great and growing community surrounding Rust. This ranges from the aforementioned official book, to an open development process that you can participate in, to IRC and Gitter channels where you can get expert friendly help at any hour of the day. Even though Rust is billed as a "system level language", one of its goals is to bring low level programming to the masses. Because of that, the community is a warm and welcoming one filled with many budding developers.

## Why not libtcod?

.shrug

## Who is this tutorial for?

It is recommended to have some familiarity with programming in general. While there will be an attempt to discuss and link to the relevent sections in the Rust Book as new Rust specific concepts come up, there won't be in-depth explainations of fundamental programming concepts like functions, control flow and the like. If you're in doubt, why not give the first couple chapters a shot? If you're in over your head please file an issue, then maybe give the Python tutorial a try, but be sure to come back at some point!

## Some notes

* Code listings prepended by a `$` are meant to be typed into the terminal. Code listings without are meant to be read and understood.

Alright, enough of this, lets get started!
