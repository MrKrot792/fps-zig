A lightweigth FPS module.

# Features
- delta
- FPS
- Real FPS (updates every second)

# How to use
1. Fetch this module into your project:
```bash
zig fetch --save git+https://github.com/MrKrot792/fps-zig
```

2. Add this to your `build.zig`:
```zig
const fps_dep = b.dependency("fps", .{
    .target = target,
    .optimize = optimize,
});

exe.root_module.addImport("fps", fps_dep.module("fps"));
```

3. Use it in your project like this (this is just an example):
```zig
const std = @import("std");
const fps = @import("fps");
const game = @import("game");

pub fn loop() !void {
    var timer: fps.Timer = try .start();
    var fps_info: fps.FpsInfo = .zero;

    while (game.running()) {
        fps.frameStart(&timer);
        game.draw(fps_info);
        fps_info = fps.frameEnd(&timer);
    }
}
```
