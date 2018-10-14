# README
## Table of Contents

 - [Introduction](#intro)
 - [Technologies](#tech)
 - [Hardware](#hard)
 - [Platforms](#platforms)

## Intro  <a name="intro"></a>

Knowledge collection repo, MarkDown(MD) based. It will include my conspects on key technologies and platforms, some of them is digital form of old paper-based notes.

## Technologies: <a name="tech"></a>
 - [OpenGL](OpenGL/README.md);
 - Vulkan;
 - [OpenCV](OpenCV/README.md);
 - Qt;
 - OpenCL/CUDA;

## Hardware: <a name="hard"></a>

### Boards:
 - [All boards](Hardware/README.md)
 - [Tegra K1](Hardware/tegraK1.md)
 - [Raspberry Pi](Hardware/rpicompute.md);

## Platforms: <a name="platforms"></a>

### Mobile

- iOS;
- Android;
- Blackberry OS10;

### Desktop 
 
 - Linux;
 - Windows;
 - OSX;


## Issues with QOwnNotes <a name="qownnotes"></a>

- QOnwNotes **automatically** rename file to the 1st level header (thats why this one have `# README` on top)
- image link use local file
- do not use a QOwnNotes link to notes - only direct with html tag
    - i.e. `[OpenCV.md#type]`;
- `tag` is not clear implemented in MD, while supported localy by QOnwNotes. Need to find a better solution.
