# Aerospace

- AeroSpace is a tiling window manager for macOS similar to [i3](https://i3wm.org) / [Sway](https://swaywm.org/)
   - Source: https://nikitabobko.github.io/AeroSpace/
   - Docs / Guide: https://nikitabobko.github.io/AeroSpace/guide
- Keyboard centric but can use mouse as well
- Has own spaces / workspace / virtual desktop implementation to allow instant switching compared to macOS forced animations 
- i3/Sway users: see note at the bottom for quick comparison
- Known Issues
   - Some applications (e.g. Terminal, Finder) reports tabs as windows causing weird behaviours so workaround is to use them as windows instead of tabs https://github.com/nikitabobko/AeroSpace/issues/68 
   - Reports of performance issues occasionally

## Main / Service binding modes
- A binding mode allows a different sent of shortcuts/binds based on mode
- Each bind mode will have its own set of shortcuts and the current bind mode will show up as extra text in the menu icon if it is not the default mode
- Default mode: `main`
   - used for most window manipulations
   - layout toggles
   - focusing/moving windows
   - moving windows to workspaces
   - focusing workspaces
- Service mode
   - shows as `[S]`
   - Main use would be to join/combine windows to allow creation of a new layout
- Main modifier key is `alt` a.k.a. `option`

## Default / Main mode shortcuts
- `alt` + `shift` + `semicolon`: enter service mode
- Window related:
   - `alt` + `slash`: tiling layout (repeat to toggle between horizontal/vertical)
   - `alt` + `comma`: accordion layout (repeat to toggle between horizontal/vertical)
   - `alt` + `h`: focus window left
   - `alt` + `j`: focus window down / below
   - `alt` + `k`: focus window up / above
   - `alt` + `l`: focus window right
   - `alt` + `shift` + `h`: move window left
   - `alt` + `shift` + `j`: move window down
   - `alt` + `shift` + `k`: move window up
   - `alt` + `shift` + `l`: move window right
   - `alt` + `minus`: smart resize (auto selects dimension) - decrease dimension
   - `alt` + `equal`: smart resize (auto selects dimension) - increase dimension
- Workspace related:
   - `$workspaceID` valid values: `1`-`9`,`a`-`z` (excluding `h`,`j`,`k`,`l` as used for navigation)
   - `alt` + `$workspaceID`: switch to workspace
   - `alt` + `shift` + `$workspaceID`: move window to workspace
   - `alt` + `tab`: toggle between last workspace
   - `alt` + `shift` + `tab`: move workspace to next monitor

### Suggested custom resize shortcuts
- As a complement to existing shortcuts. Uses an extra `shift` key to toggle the other dimension
```
alt-shift-minus = 'resize smart-opposite -50'
alt-shift-equal = 'resize smart-opposite +50'
```

## [S] Service mode shortcuts

- `esc`: reload config and exit service mode
- `r`: reset layout
- `f`: toggle floating window (double click floating window to toggle fullscreen)
- Combining / Joining windows:
   - After combining can toggle the layout of the new container
   - `alt` + `shift` + `h`: join with window to the left 
   - `alt` + `shift` + `j`: join with window below 
   - `alt` + `shift` + `k`: join with window above 
   - `alt` + `shift` + `l`: join with window to the right 
   

## Note for i3/Sway users
- Similar in terms of layout concepts
   - i3/sway: splith/splitv => Aerospace: tiled horizontal/vertical
   - i3/sway: stacking/tabbed => Aerospace: accordian horizontal/vertical
- Also has binding modes
- Workspaces not limited by numbers
- No extra window decoration / titlebar to easily visualize layouts
   - Mostly an issue with accordians
   - Accordians do shown the windows to the left/right (horizontal accordian) or above/below (vertical accordian) current window as a little sliver to help indicate that they exist
- Creating and manipulating layouts harder to do
- No fullscreen by default
- Floating windows are still focusable