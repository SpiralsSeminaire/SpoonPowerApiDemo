Demo of Spoon and PowerApi
==========================

This project contains the demo which uses Spoon and PowerApi together on open source projects.

Demos
-----

You can launch 2 demos: vraptor and ninja

```bash
docker build -t spoon/vraptor vraptor
docker run -i -t spoon/vraptor /bin/bash
```

```bash
docker build -t spoon/ninja ninja
docker run -i -t spoon/ninja /bin/bash
```

These commands create a docker image to configure the open source project vraptor or ninja with all dependencies needed.

In another terminal, you must launch powerapi on the java pid:

```bash
./bin/powerapi modules sigar-cpu-simple monitor --frequency 250 --targets java --chart
```

In the terminal connected in your docker image, you can execute some maven commands according to profiles configured in these projects:

> **Note:** Projects are in `/root/project`.

original compile:

```bash
mvn clean install -fn
```

spoon compile:

```bash
mvn clean install -P spoon -fn
```

diversify compile:

```bash
mvn clean install -P diversify-all -fn
```

Enjoy!