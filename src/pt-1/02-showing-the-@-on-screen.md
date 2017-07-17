# Showing the `@` on screen

This next section (like the Python version) will be a bunch of copy and pasting of boilerplate. It isn't fully necessary to understand all of it. I'll go over the relevent bits and we'll get on our way to the more interesting bits once we get something on the screen.

Now that we have our needed libraries in our `Cargo.toml` we'll import them into our current scope (`main.rs`) using the following on the first line of the file (above the `fn main() {` portion):

```rust
extern crate glium;
extern crate gltile;
extern crate looper;
extern crate pixset;
```

Right below all the `extern`s we'll import some names into our scope to reduce the typing we need to do:

```rust
use gltile::colors;
use pixset::Pix;
```

`glium`, our OpenGL library, needs to create a window for us to draw on, and in order to do so it needs the size of the window to create, in pixels. Since we're using a tileset with 16x16 pixel tiles and want a window with a width of 80 tiles and height of 50 tiles, we'll need a window with 1,280 pixels wide and 800 pixels tall. The rest is just boilerplate to get things up and running. Ultimately all we care about is the `renderer` that we get from the last line. Note that we pass the renderer `pixset::TILESET`, which gives us the default tileset provided by the `pixset` crate along with the `Empty` tile from that `TILESET` which the renderer uses to initialize a blank screen. All of this code goes inside the `main` function.

```rust
let mut events_loop = glium::glutin::EventsLoop::new();
let window = glium::glutin::WindowBuilder::new().with_dimensions(1_280, 800);
let context = glium::glutin::ContextBuilder::new();
let display = glium::Display::new(window, context, &events_loop).unwrap();
let mut renderer = gltile::Renderer::new(&display, &pixset::TILESET);
```

After we've got our renderer we'll make a tile for our hero, the `@` symbol:


```rust
let tile = gltile::Tile::make(
    *colors::WHITE,
    *colors::BLACK,
    Pix::Ampersand,
);
```

The first arguement to `Tile::make` is the foreground color, and the second arguement is the background color. Finally, the third argument is the symbol to use. /* TODO */ point to full listing of `pixset` tiles.

Then we'll set the 1st tile to the right, and the 1st tile down to our hero. Coordinates start from the top left corner and proceed to the right and down. We're passing in a tuple to denote the x and y coordinates.

```rust
renderer.set((1, 1), tile);
```

After that is another block of boilerplate. An instance of `looper` is created at the bottom and is passed both a render closure and an update closure, which is called at `60.0` FPS in an alternating fashion.

```rust
let render = |_| {
    renderer.render();
    looper::Action::Continue
};

let update = |_| {
    let mut action = looper::Action::Continue;
    events_loop.poll_events(|event| match event {
        glium::glutin::Event::WindowEvent { event, .. } => {
            match event {
                glium::glutin::WindowEvent::Closed => action = looper::Action::Stop,
                _ => (),
            }
        }
        _ => (),
    });

    action
};

looper::Looper::new(60.0).run(render, update);
```
