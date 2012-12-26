---
title: "OASIS builds with camlp4"
layout: post
published: false
---

As of v0.3.0, OASIS is not camlp4-aware. However, the underlying
ocamlbuild system *is* camlp4-aware, so it's possible to build with
camlp4 by reaching through the OASIS abstraction layer into ocamlbuild:

1.  manually edit the `_tags` file to add the `syntax(camlp4o)` tag to
whatever files need the preprocessing:

        # this works for me; yours may vary
        <\*/\*.ml{,i}>: syntax(camlp4o)

        # OASIS_START
        # ... gets replaced when OASIS regenerates the _tags file
        # OASIS_STOP

2.  pass ocamlbuild the `-use-ocamlfind` flag, like so:

        ocaml setup.ml -build -use-ocamlfind

This is based on advice from Le Gall in a
[2010 OASIS-devel thread](https://lists.forge.ocamlcore.org/pipermail/oasis-devel/2010-October/000004.html).
