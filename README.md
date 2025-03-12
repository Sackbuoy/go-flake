# Go nix flake
A simple nix flake to pull in various versions of Go

## Example
```
{
  description = "Go Development flake";

  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
    go-flake.url = "github:Sackbuoy/go-flake";
  };

  outputs = {
    self,
    nixpkgs,
    go-flake,
  }: let
    system = "x86_64-linux";
    pkgs = nixpkgs.legacyPackages.${system};

    go = go-flake.packages.${system}.go-1-23-6;
  in {
    devShells.${system}.default = pkgs.mkShell {
      buildInputs = [
        go
      ];

      shellHook = ''
        echo "Golang development environment with go v1.23.6"
      '';
    };
  };
}

```
