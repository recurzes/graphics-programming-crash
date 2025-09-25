# Project Structure:
```bash
.
├── chapters
│   ├── simple_point
│   │   └── simple_point.cpp
│   └── simple_window
│       └── simple_window.cpp
├── CMakeLists.txt
└── README.md
```
- When adding a new file, you need to make the name of the folder and the source file be identical to avoid errors on cmake build

# Building:
- Create a "build" folder on the root project
- cd into build folder
- "cmake --build . --target 'name_of_the_folder'"
- "make"
### And your binary is built fucking magic
