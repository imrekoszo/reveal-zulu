# reveal-zulu

This is to create a (hopefully) minimal repro case for an issue I had running [Reveal](https://vlaaad.github.io/reveal/) on [Zulu JDK8 + JavaFX](https://www.azul.com/downloads/zulu-community/?os=macos&architecture=x86-64-bit&package=jdk-fx).

The problem seems to only come out when I run this from [Cursive](https://cursive-ide.com/).

## Repro steps

### Get Zulu JDK8 with JavaFX

I used [sdkman](https://sdkman.io/):

```shell
sdk install java 8.0.282.fx-zulu
```

In the root of this project:

```shell
> sdk env
> sdk current java

Using java version 8.0.282.fx-zulu
```

### Works: run from the command line

```shell
clj -Sforce 
```

In the repl:

```clojure
(do (require 'vlaaad.reveal) (add-tap (vlaaad.reveal/ui)))
```

Reveal window appears.

### Does not work: run from Cursive

Using

```text
IntelliJ IDEA 2020.3.4 (Community Edition)
Build #IC-203.8084.24, built on April 27, 2021
Runtime version: 11.0.10+8-b1145.96 x86_64
VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
macOS 10.16

Cursive 1.10.2-2020.3
```

1. Add new local REPL Run config
2. Run it
3. `(do (require 'vlaaad.reveal) (add-tap (vlaaad.reveal/ui)))`

Reveal window does not appear, the following error is printed:

```text
Syntax error (IllegalArgumentException) compiling . at (cljfx/jdk/platform.clj:6:5).
No matching method startup found taking 1 args for class javafx.application.Platform
```
