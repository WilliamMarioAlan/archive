# Shared Object(动态库).so(Shared Object)

g++ -shared -o libmath_utils.so math_utils.o 

### **`.so`：动态库 (Shared Object)**

- **全称**：Shared Object。
- **特点**：
    - 动态库在运行时被加载到内存中。
    - 在**编译阶段**，只需要告诉链接器在哪里可以找到动态库。
    - 一个动态库可以同时被多个程序共享使用。
    - 如果动态库更新，无需重新编译链接程序，程序可以直接使用最新的库。
    - 依赖动态库的程序运行时需要确保动态库可以被找到（通过环境变量 `LD_LIBRARY_PATH` 或系统默认路径 `/usr/lib`, `/lib` 等）。
- **优点**：
    - 减少可执行文件的体积，因为库内容没有嵌入。
    - 多个程序可以共享同一个动态库，减少内存占用。
    - 更新库文件后，程序可以立即使用新的功能。
- **缺点**：
    - 程序运行时依赖动态库的存在。
    - 如果动态库路径出错或文件丢失，程序将无法运行。
- **创建动态库**：
    1. 编译目标文件：
        
        ```bash
        gcc -fPIC -c mylib.c -o mylib.o
        
        ```
        
        - `fPIC` 表示生成位置无关代码，便于动态库加载。
    2. 生成动态库：
        
        ```bash
        gcc -shared -o libmylib.so mylib.o
        
        ```
        
    3. 使用动态库：
        
        ```bash
        gcc main.c -L. -lmylib -o myprogram
        export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:.
        ./myprogram
        
        ```
        
        - `LD_LIBRARY_PATH`：指定动态库路径。

---