# OBJECTS = $(SOURCES:.cpp=.o)解释

`OBJECTS = $(SOURCES:.cpp=.o)` 是一种主流且通用的写法，用于将源文件列表转换为目标文件列表。它利用了 **GNU Make** 的**模式替换**语法，简洁、高效，广泛应用于 Makefile 的编写中。

---

### **解析这段代码的含义**

- **`SOURCES`**：通常表示源文件列表（如 `.cpp` 文件）。
- **`OBJECTS`**：表示生成的目标文件列表（如 `.o` 文件）。
- **`$(SOURCES:.cpp=.o)`**：将 `SOURCES` 中的每个 `.cpp` 文件替换为对应的 `.o` 文件。

### **示例**

假设：

```makefile
SOURCES = main.cpp utils.cpp
OBJECTS = $(SOURCES:.cpp=.o)

```

执行后，`OBJECTS` 将展开为：

```
OBJECTS = main.o utils.o

```

---

### **为什么这是主流写法？**

1. **简洁性**
    - 避免了手动列出 `.o` 文件，减少重复性工作。
    - 如果源文件列表有变动，只需要维护 `SOURCES`，无需单独修改 `OBJECTS`。
2. **自动化程度高**
    - 与通用的模式规则结合使用，可以极大简化 Makefile 的编写。
    
    ```makefile
    SOURCES = main.cpp utils.cpp
    OBJECTS = $(SOURCES:.cpp=.o)
    
    %.o: %.cpp
        g++ -c $< -o $@
    
    ```
    
    只需维护 `SOURCES`，其余自动完成。
    
3. **便于扩展**
    - 如果源文件类型发生变化（如从 `.cpp` 转为 `.c`），只需修改 `SOURCES` 和对应规则，`OBJECTS` 会自动适配。
4. **兼容性强**
    - 这种写法适用于大多数常见的 Make 实现（包括 GNU Make），且简单直观。

---

### **模式替换的通用语法**

### 基本形式

```makefile
$(变量名:模式1=模式2)

```

- **`模式1`**：指定替换前的模式。
- **`模式2`**：指定替换后的模式。

### 示例用法

1. **简单替换扩展名**
    
    ```makefile
    SOURCES = file1.c file2.c file3.c
    OBJECTS = $(SOURCES:.c=.o)
    
    ```
    
    - 将 `.c` 文件转换为 `.o` 文件。
2. **更复杂的路径替换**
    
    ```makefile
    SOURCES = src/file1.c src/file2.c
    OBJECTS = $(SOURCES:src/%.c=build/%.o)
    
    ```
    
    - 将源文件路径从 `src/` 转换为目标文件路径 `build/`。
3. **结合变量和路径**
    
    ```makefile
    SRCDIR = src
    OBJDIR = build
    SOURCES = $(SRCDIR)/main.cpp $(SRCDIR)/utils.cpp
    OBJECTS = $(SOURCES:$(SRCDIR)/%.cpp=$(OBJDIR)/%.o)
    
    ```
    

---

### **主流和更高级的用法**

在实际项目中，这种写法可能会与工具链和自动化规则结合，比如使用通用规则动态生成目标文件列表：

### **（1）动态生成源文件列表**

```makefile
SOURCES = $(wildcard *.cpp)
OBJECTS = $(SOURCES:.cpp=.o)

```

- **`$(wildcard *.cpp)`**：自动搜集当前目录下的所有 `.cpp` 文件。
- 不需要手动维护 `SOURCES`。

### **（2）结合子目录结构**

```makefile
SRCDIR = src
OBJDIR = build
SOURCES = $(wildcard $(SRCDIR)/*.cpp)
OBJECTS = $(patsubst $(SRCDIR)/%.cpp, $(OBJDIR)/%.o, $(SOURCES))

```

- 使用 `$(patsubst)` 替换路径和扩展名，适应复杂的目录结构。

### **（3）结合自动依赖管理**

通过这种写法，可以结合 `.d` 文件（依赖文件）生成更强大的 Makefile：

```makefile
SOURCES = main.cpp utils.cpp
OBJECTS = $(SOURCES:.cpp=.o)

%.o: %.cpp
    g++ -MMD -c $< -o $@

-include $(OBJECTS:.o=.d)

all: $(OBJECTS)
    g++ $^ -o program

```

- **`MMD`**：生成 `.d` 文件（记录依赖关系）。
- **`include`**：包含 `.d` 文件，确保自动检测文件依赖。

---

### **总结**

`OBJECTS = $(SOURCES:.cpp=.o)` 是主流且推荐的写法，原因在于：

- 简单直观，易于维护。
- 与模式规则和自动化变量结合，能大幅减少重复代码。
- 在大多数主流项目中应用广泛，可以作为编写高效 Makefile 的基础技巧。