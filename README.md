# README

## Intro 

Knowledge collection repo, MarkDown(MD) based. It will include my conspects on key technologies and platforms, some of them is digital form of old paper-based notes.

## Technologies:
 - [OpenGL](OpenGL/README.md);
 - Vulkan;
 - [OpenCV](OpenCV/README.md);
 - Qt;
 - OpenCL/CUDA;

## Platforms:

### Mobile

- iOS;
- Android;
- Blackberry OS10;

### Desktop 
 
 - Linux;
 - Windows;
 - OSX;

### Boards
 - [Raspberry Pi](RaspberryPi/README.md);
 - ESP8266;
 
## Issues with QOwnNotes

- QOnwNotes **automatically** rename file to the 1st level header (thats why this one have `# README` on top)
- image link use local file
- do not use a QOwnNotes link to notes - only direct with html tag
    - i.e. `[OpenCV.md#type]`;
- `tag` is not clear implemented in MD, while supported localy by QOnwNotes. Need to find a better solution.
