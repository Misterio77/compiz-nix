# Compiz 0.9 on Nix

This is [Compiz 0.9.x](https://code.launchpad.net/compiz) packaged for NixOS.

TODO:
- [x] Compiz (Full)
- [ ] Emerald (Full)

Tragically, Nix decided to remove Compiz from nixpkgs like ages ago. This was the only thing stopping me from migrating to NixOS (since I use compiz at least until I can make my own wayland wm :3), so now compiz is back on the nix land!

This is a fork of [Gabriel's repo](https://github.com/Misterio77/compiz-nix). He's like the proest of pros when it comes to nix, and he did most of the work packaging this!


## Installing

Add this repo to your flake inputs on your `flake.nix`:
````nix
    compiz.url = "github:LuNeder/compiz-reloaded-nix/compiz09";
    compiz.inputs.nixpkgs.follows = "nixpkgs";
````

Then install Compiz from your `environment.systemPackages`:
````nix
inputs.compiz.packages.${pkgs.system}.default
````

## Using

You now should be able to launch Compiz from a terminal with `compiz --replace`.

If you use XFCE and want to use Compiz as your compositor/window manager, you can add the following to your Home-Manager config to autostart it:

````nix
    # Autostart Compiz
    xfconf.settings = {
      xfce4-session."sessions/Failsafe/Client1_Command" = [ "xfsettingsd" ];
      xfce4-session."sessions/Failsafe/Client0_Command" = [ "compiz" ];
    };
````

## Configuring

You can configure Compiz from CompizConfig (CCSM). Run `ccsm` from your terminal or find it in your menu or something.
For now there's no way to configure Compiz directly from Nix but ccsm is really cool (if you want to share your Compiz configuration you can export (and import) it from ccsm).

#### Note

Compiz will launch the `gtk-window-decorator` window decorator on startup by default. If you don't like it, you can change this for your favourite decorator on ccsm. I'll package Emerald someday which will probably be a better fit.

## Compiz-Reloaded
I'm also trying to package compiz-reloaded since Compiz 0.9 has some weird bugs (unlike compiz 0.8 / [compiz-reloaded](https://gitlab.com/compiz/compiz-core)), but that's still a wip (see the [main](https://github.com/LuNeder/compiz-reloaded-nix/tree/main) branch of this repo).
