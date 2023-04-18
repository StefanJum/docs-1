---
title: "01 - Build System"
date: 2023-04-12T01:10:00+02:00
draft: false
weight: 1
---

## Challenge Description

You are given the following file structure:

```console
.
|-- key.c
|-- main.c
`-- some
    `-- far
        `-- away
            |-- include
            |   `-- myheader.h
            `-- src
                `-- values.c
```

Your task is to create a `Makefile` that will be used to build everything into an executable file.
After everything is done, if you run the executable you will find a flag:

```console
$ ./main
[...]
USoC{...}
```

Copy that flag and paste it in the [registration form](https://forms.gle/Lz3DqefrnfxWFMCB8), then create an archive with all the files (`Makefile` and other helper files) that are required to build the given sources.

## Resources

You can find a basic tutorial on building a `Makefile` [here](https://cs.colby.edu/maxwell/courses/tutorials/maketutor/), and a more detailed example [here](https://makefiletutorial.com/).
