some edwards curves (curve1174, curve41417, x448) in
[cryptol](https://cryptol.net). `Curve.cry` defines the generalized
implementation for scalar multiplication over a twisted edwards curve with
user-chosen parameters. the other various modules instantiate to various
concrete parameter choices.

point compression does not work; it's probably entirely wrong. random points
for testing are generated via base point multiplication with a random scalar,
not randomized/invalid curve points -- a common flaw in many implementations.
small subgroup attacks are prevented with masking scalar bits to a multiple of
the cofactor, and scalar clamping is done to set the top-most bit for the
ladder, but i haven't double checked all this is correct in all cases. (this
code was originally derived from an old sketch i had of montgomery curves, but
modified to use edwards curves only)

it may, however, be useful when i need to jog my memory. when in doubt, the
[safecurves website](https://safecurves.cr.yp.to) probably has all the needed
information.

do not use.

#### go go gadget arms

```
nix run \
  -I nixpkgs=https://github.com/NixOS/nixpkgs-channels/archive/baa75f0c25a26ba7423d46ae2b9e89b62dc149e3.tar.gz \
  nixpkgs.cryptol -c \
  cryptol -c ':l X41417.cry' -c ':check'
```
