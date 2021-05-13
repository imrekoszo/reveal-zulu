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
IntelliJ IDEA 2021.1.1 (Community Edition)
Build #IC-211.7142.45, built on April 30, 2021
Runtime version: 11.0.10+9-b1341.41 x86_64
VM: Dynamic Code Evolution 64-Bit Server VM by JetBrains s.r.o.
macOS 11.3.1

Cursive 1.10.2-2021.1
```

1. Ensure the project is using the `8.0.282.fx-zulu` JDK 
2. Add new local REPL Run config
3. Run it
4. `(do (require 'vlaaad.reveal) (add-tap (vlaaad.reveal/ui)))`

Reveal window does not appear, the following error is printed:

```text
Syntax error (IllegalArgumentException) compiling . at (cljfx/jdk/platform.clj:6:5).
No matching method startup found taking 1 args for class javafx.application.Platform
```

Problem persists even after cache invalidation/restart.
