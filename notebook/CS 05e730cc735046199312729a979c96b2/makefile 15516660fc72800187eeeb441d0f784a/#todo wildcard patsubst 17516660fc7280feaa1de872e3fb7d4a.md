# #todo wildcard patsubst

Makefile 是构建自动化构建系统的重要工具，而内置函数是其核心功能之一。以下将详细解释 **`wildcard`** 和 **`patsubst`** 的用法，并总结主流高频函数及其典型应用场景，帮助你高效掌握 Makefile 的编写技巧。

---

## **1. `wildcard` 函数**

**功能**：匹配符合指定模式的文件，并返回以空格分隔的文件路径列表。

### **语法**

```makefile
$(wildcard pattern)

```

- **参数**：
    - `pattern`：文件匹配模式，支持通配符。
        - ``：匹配任意字符。
        - `?`：匹配单个字符。
        - `[set]`：匹配集合中的任意字符。
    - 支持递归匹配（如 `*/*.c`）。

### **示例**

```makefile
# 获取当前目录中的所有 .c 文件
SRC_FILES = $(wildcard *.c)

# 获取 src/ 目录中的所有 .cpp 文件
CXX_FILES = $(wildcard src/*.cpp)

# 获取所有子目录中的 .h 文件
HEADERS = $(wildcard src/**/*.h)

```

### **常见应用**

1. 自动搜索源文件：
    
    ```makefile
    SRCS = $(wildcard src/*.c src/*.cpp)
    
    ```
    
2. 动态适配文件变化：
    
    ```makefile
    # 自动更新目录中的头文件
    HEADERS = $(wildcard include/*.h)
    
    ```
    

---

## **2. `patsubst` 函数**

**功能**：将字符串中的部分内容替换为指定内容，通常用于路径和文件名的转换。

### **语法**

```makefile
$(patsubst pattern,replacement,text)

```

- **参数**：
    - `pattern`：匹配规则，`%` 作为通配符，表示任意字符。
    - `replacement`：替换内容，`%` 保留与 `pattern` 中 `%` 匹配的部分。
    - `text`：待处理的字符串。

### **示例**

```makefile
# 将 src/ 中的 .c 文件转换为 build/ 中的 .o 文件
OBJECTS = $(patsubst src/%.c, build/%.o, $(wildcard src/*.c))

# 替换文件扩展名
OBJS = $(patsubst %.cpp, %.o, $(wildcard *.cpp))

# 替换路径前缀
NEW_PATHS = $(patsubst old_dir/%, new_dir/%, $(wildcard old_dir/*))

```

### **常见应用**

1. **源文件到目标文件路径的转换**：
    
    ```makefile
    # 生成 .o 文件路径
    OBJECTS = $(patsubst %.c, %.o, $(SRCS))
    
    ```
    
2. **路径前缀修改**：
    
    ```makefile
    BUILDS = $(patsubst src/%, build/%, $(SRCS))
    
    ```
    

---

## **3. 高频函数详解**

以下是 Makefile 中最常用的函数：

### **3.1 `wildcard`**

- **作用**：查找文件。
- **用法**：
    
    ```makefile
    SRCS = $(wildcard src/*.c src/*.cpp)
    
    ```
    

### **3.2 `patsubst`**

- **作用**：路径和文件名的替换。
- **用法**：
    
    ```makefile
    OBJECTS = $(patsubst src/%.cpp, build/%.o, $(SRCS))
    
    ```
    

### **3.3 `subst`**

- **功能**：简单的字符串替换，不支持通配符。
- **语法**：
    
    ```makefile
    $(subst from,to,text)
    
    ```
    
- **示例**：
    
    ```makefile
    # 替换路径分隔符
    NEW_PATHS = $(subst /,\\,$(SRCS))
    
    ```
    

### **3.4 `addprefix` 和 `addsuffix`**

- **功能**：为字符串列表添加前缀或后缀。
- **语法**：
    
    ```makefile
    $(addprefix prefix,text)
    $(addsuffix suffix,text)
    
    ```
    
- **示例**：
    
    ```makefile
    SRCS = main.c utils.c
    FULL_PATHS = $(addprefix src/, $(SRCS))
    OBJECTS = $(addsuffix .o, $(basename $(SRCS)))
    
    ```
    

### **3.5 `basename` 和 `notdir`**

- **`basename`**：获取文件名的基础名（去掉后缀）。
- **`notdir`**：去掉路径部分，仅保留文件名。
- **示例**：
    
    ```makefile
    # 假设文件路径是 src/main.cpp
    BASENAME = $(basename src/main.cpp)    # 结果是 src/main
    NOTDIR = $(notdir src/main.cpp)        # 结果是 main.cpp
    
    ```
    

### **3.6 `dir`**

- **功能**：提取路径部分。
- **示例**：
    
    ```makefile
    DIR = $(dir src/main.cpp)    # 结果是 src/
    
    ```
    

### **3.7 `filter` 和 `filter-out`**

- **功能**：从字符串中筛选或排除特定模式。
- **语法**：
    
    ```makefile
    $(filter pattern,text)
    $(filter-out pattern,text)
    
    ```
    
- **示例**：
    
    ```makefile
    FILES = main.cpp utils.cpp main.h utils.h
    CPP_FILES = $(filter %.cpp, $(FILES))    # 结果是 main.cpp utils.cpp
    HEADER_FILES = $(filter-out %.cpp, $(FILES))    # 结果是 main.h utils.h
    
    ```
    

### **3.8 `sort` 和 `uniq`**

- **功能**：排序和去重。
- **示例**：
    
    ```makefile
    ITEMS = b a c a b
    SORTED = $(sort $(ITEMS))    # 结果是 a b c
    
    ```
    

### **3.9 `shell`**

- **功能**：执行 Shell 命令并返回结果。
- **语法**：
    
    ```makefile
    $(shell command)
    
    ```
    
- **示例**：
    
    ```makefile
    DATE = $(shell date)
    
    ```
    

---

## **4. 综合示例：自动化构建系统**

以下是一个完整的 Makefile 示例，演示如何结合以上函数实现自动化构建：

```makefile
# 定义变量
CXX = g++
CXXFLAGS = -std=c++17 -Wall -Wextra -g -Iinclude
SRCDIR = src
BUILDDIR = build

# 自动查找文件
SRCS = $(wildcard $(SRCDIR)/*.cpp)
OBJS = $(patsubst $(SRCDIR)/%.cpp, $(BUILDDIR)/%.o, $(SRCS))
TARGET = app

# 规则
all: $(TARGET)

$(TARGET): $(OBJS)
	$(CXX) $(CXXFLAGS) -o $@ $^

$(BUILDDIR)/%.o: $(SRCDIR)/%.cpp
	mkdir -p $(BUILDDIR)
	$(CXX) $(CXXFLAGS) -c $< -o $@

clean:
	rm -rf $(BUILDDIR) $(TARGET)

.PHONY: all clean

```

---

## **5. 高效学习建议**

1. **熟练使用高频函数**：如 `wildcard`、`patsubst`、`subst`、`addprefix`。
2. **逐步学习复杂功能**：从简单的变量替换到路径管理。
3. **实践是关键**：
    - 模仿优秀项目的 Makefile。
    - 动手编写小型项目的 Makefile。
4. **借助工具**：
    - 使用 GNU Make 官方文档。
    - 在线调试工具（如 Makefile Linter）。

通过实践和理解这些函数，能够大幅提升编写 Makefile 的效率和灵活性。

以下是 **Makefile** 中提到的函数全称以及其用途的详细说明：

---

### **1. `wildcard`**

**全称**：`wildcard`

**功能**：用于匹配指定模式的文件，类似于 Shell 的文件通配符匹配。

**示例**：

```makefile
FILES = $(wildcard src/*.c)

```

---

### **2. `patsubst`**

**全称**：`pattern substitution`（模式替换）

**功能**：基于通配符模式的字符串替换。

**示例**：

```makefile
OBJECTS = $(patsubst %.c, %.o, $(SOURCES))

```

---

### **3. `subst`**

**全称**：`substitution`（替换）

**功能**：简单的字符串替换，不支持通配符。

**示例**：

```makefile
NEW_PATHS = $(subst src, build, $(FILES))

```

---

### **4. `addprefix`**

**全称**：`add prefix`（添加前缀）

**功能**：为字符串列表中的每一项添加指定前缀。

**示例**：

```makefile
SRC_FILES = main.c utils.c
FULL_PATHS = $(addprefix src/, $(SRC_FILES))  # src/main.c src/utils.c

```

---

### **5. `addsuffix`**

**全称**：`add suffix`（添加后缀）

**功能**：为字符串列表中的每一项添加指定后缀。

**示例**：

```makefile
OBJS = $(addsuffix .o, $(basename $(SRC_FILES)))

```

---

### **6. `basename`**

**全称**：`base name`（基础名）

**功能**：从文件路径中去掉扩展名，返回文件基础名。

**示例**：

```makefile
BASE = $(basename src/main.c)  # 结果是 src/main

```

---

### **7. `notdir`**

**全称**：`not directory`（非目录）

**功能**：去掉路径部分，仅保留文件名。

**示例**：

```makefile
NAME = $(notdir src/main.c)  # 结果是 main.c

```

---

### **8. `dir`**

**全称**：`directory`（目录）

**功能**：返回文件路径中的目录部分。

**示例**：

```makefile
DIR = $(dir src/main.c)  # 结果是 src/

```

---

### **9. `filter`**

**全称**：`filter`（过滤）

**功能**：保留字符串列表中符合模式的部分。

**示例**：

```makefile
CPP_FILES = $(filter %.cpp, $(FILES))  # 结果是所有 .cpp 文件

```

---

### **10. `filter-out`**

**全称**：`filter out`（过滤排除）

**功能**：排除字符串列表中符合模式的部分。

**示例**：

```makefile
NON_CPP_FILES = $(filter-out %.cpp, $(FILES))

```

---

### **11. `sort`**

**全称**：`sort`（排序）

**功能**：对字符串列表排序，并自动去重。

**示例**：

```makefile
SORTED = $(sort c b a c)  # 结果是 a b c

```

---

### **12. `shell`**

**全称**：`shell`（Shell 命令）

**功能**：执行 Shell 命令，并返回输出结果。

**示例**：

```makefile
DATE = $(shell date)  # 获取当前日期

```

---

### **13. `wildcard`**

**全称**：`wildcard`（通配符匹配）

**功能**：查找符合指定模式的文件列表。

**示例**：

```makefile
FILES = $(wildcard src/*.c)  # 匹配 src/ 中的所有 .c 文件

```

---

### **14. `foreach`**

**全称**：`foreach`（遍历）

**功能**：对列表中的每一项执行某些操作。

**语法**：

```makefile
$(foreach var,list,text)

```

- `var` 是当前变量名。
- `list` 是待遍历的列表。
- `text` 是对每项执行的操作。

**示例**：

```makefile
RESULT = $(foreach file,$(FILES),$(shell cp $(file) $(TARGET_DIR)))

```

---

### **15. `if`**

**全称**：`if`（条件判断）

**功能**：在 Makefile 中实现简单的条件判断。

**语法**：

```makefile
$(if condition,then-part[,else-part])

```

**示例**：

```makefile
RESULT = $(if $(wildcard $(FILE)),exists,missing)

```

---

### **16. `error`**

**全称**：`error`（报错）

**功能**：在构建过程中抛出错误，终止构建。

**示例**：

```makefile
$(error Missing source file)

```

---

### **17. `warning`**

**全称**：`warning`（警告）

**功能**：抛出警告信息，但不终止构建。

**示例**：

```makefile
$(warning Deprecated feature)

```

---

### **18. `call`**

**全称**：`call`（调用函数）

**功能**：定义和调用自定义函数。

**语法**：

```makefile
$(call name,param1,param2,...)

```

**示例**：

```makefile
# 定义函数
reverse = $(2) $(1)

# 调用函数
RESULT = $(call reverse,a,b)  # 结果是 b a

```

---

## **常见高效组合**

1. **自动化文件管理**：
    
    ```makefile
    SRCS = $(wildcard src/*.cpp)
    OBJS = $(patsubst src/%.cpp, build/%.o, $(SRCS))
    
    ```
    
2. **路径调整**：
    
    ```makefile
    FULL_PATHS = $(addprefix src/, main.cpp utils.cpp)
    
    ```
    
3. **筛选和排除**：
    
    ```makefile
    CPP_FILES = $(filter %.cpp, $(wildcard src/*))
    NON_HEADERS = $(filter-out %.h, $(wildcard src/*))
    
    ```
    

通过这些函数组合，你可以高效编写复杂的 Makefile 并灵活应对各种项目需求。

CXX_SOURCES = $(wildcard $(SRCDIR)/*.cpp)    # 查找所有 .cpp 文件
C_SOURCES = $(wildcard $(SRCDIR)/*.c)        # 查找所有 .c 文件
CXX_OBJECTS = $(patsubst $(SRCDIR)/%.cpp, $(BUILDDIR)/%.o, $(CXX_SOURCES))
C_OBJECTS = $(patsubst $(SRCDIR)/%.c, $(BUILDDIR)/%.o, $(C_SOURCES))详细解释

---

### **1. `CXX_SOURCES = $(wildcard $(SRCDIR)/*.cpp)`**

- **作用**：查找指定目录（`$(SRCDIR)`）下的所有 `.cpp` 文件，并将它们存储在 `CXX_SOURCES` 变量中。
- **关键点**：
    1. **`$(wildcard pattern)`**
        - Makefile 内置函数，用于匹配指定模式的文件，返回一个以空格分隔的文件列表。
        - `pattern` 是文件路径的匹配规则，例如：
            - `$(SRCDIR)/*.cpp` 匹配目录 `$(SRCDIR)` 中的所有以 `.cpp` 结尾的文件。
            - 可以使用更复杂的匹配规则，如 `$(SRCDIR)/**/*.cpp` 查找所有子目录中的 `.cpp` 文件（支持递归）。
    2. **`$(SRCDIR)`**
        - 是一个变量，代表源代码目录路径。它通常在 Makefile 中预定义，比如：
            
            ```makefile
            SRCDIR = src
            
            ```
            
    - **示例**：
    假设 `$(SRCDIR)` 是 `src`，而 `src` 目录中有以下文件：
    
    则 `CXX_SOURCES` 的值会是：
        
        ```
        main.cpp
        utils.cpp
        extra.cpp
        
        ```
        
        ```
        src/main.cpp src/utils.cpp src/extra.cpp
        
        ```
        

---

### **2. `C_SOURCES = $(wildcard $(SRCDIR)/*.c)`**

- **作用**：类似于上一行的功能，但这里查找的是 `.c` 文件。
- **关键点**：
    - `$(wildcard $(SRCDIR)/*.c)` 匹配目录 `$(SRCDIR)` 中的所有以 `.c` 结尾的文件。
    - 假设 `$(SRCDIR)` 是 `src`，而 `src` 目录中有以下文件：
    
    则 `C_SOURCES` 的值会是：
        
        ```
        main.c
        helper.c
        
        ```
        
        ```
        src/main.c src/helper.c
        
        ```
        

---

### **3. `CXX_OBJECTS = $(patsubst $(SRCDIR)/%.cpp, $(BUILDDIR)/%.o, $(CXX_SOURCES))`**

- **作用**：将 `CXX_SOURCES`（所有 `.cpp` 文件路径）转换为对应的 `.o` 文件路径，并存储在 `CXX_OBJECTS` 中。
- **关键点**：
    1. **`$(patsubst pattern,replacement,text)`**
        - Makefile 内置函数，用于对 `text` 中的每个匹配 `pattern` 的部分，按 `replacement` 替换，并返回结果。
        - `pattern` 是替换规则，`%` 表示通配符（可以匹配任意文本）。
    2. **参数含义**：
        - `$(SRCDIR)/%.cpp`：匹配 `CXX_SOURCES` 中的所有 `.cpp` 文件路径，以 `$(SRCDIR)/` 开头。
        - `$(BUILDDIR)/%.o`：将 `.cpp` 替换为 `.o`，并将路径前缀改为 `$(BUILDDIR)`。
        - `$(CXX_SOURCES)`：待处理的文本列表，存储的是所有 `.cpp` 文件路径。
    3. **示例**：
        - 假设：
            - `$(SRCDIR)` 是 `src`。
            - `$(BUILDDIR)` 是 `build`。
            - `CXX_SOURCES` 包含：`src/main.cpp src/utils.cpp`。
        - 替换过程：
            
            ```
            src/main.cpp -> build/main.o
            src/utils.cpp -> build/utils.o
            
            ```
            
        - `CXX_OBJECTS` 的值为：
            
            ```
            build/main.o build/utils.o
            
            ```
            

---

### **4. `C_OBJECTS = $(patsubst $(SRCDIR)/%.c, $(BUILDDIR)/%.o, $(C_SOURCES))`**

- **作用**：类似于上一行的功能，但这里是将 `C_SOURCES`（所有 `.c` 文件路径）转换为对应的 `.o` 文件路径。
- **关键点**：
    - 同样使用 `$(patsubst)` 将 `.c` 替换为 `.o`，并将路径前缀改为 `$(BUILDDIR)`。
    - 假设：
        - `$(SRCDIR)` 是 `src`。
        - `$(BUILDDIR)` 是 `build`。
        - `C_SOURCES` 包含：`src/main.c src/helper.c`。
    - 替换过程：
        
        ```
        src/main.c -> build/main.o
        src/helper.c -> build/helper.o
        
        ```
        
    - `C_OBJECTS` 的值为：
        
        ```
        build/main.o build/helper.o
        
        ```
        

---

### **总结**

### **变量的作用**

- `CXX_SOURCES` 和 `C_SOURCES`：分别存储 `.cpp` 和 `.c` 源文件的路径列表。
- `CXX_OBJECTS` 和 `C_OBJECTS`：分别存储 `.cpp` 和 `.c` 文件对应生成的 `.o` 文件路径列表。

### **转换逻辑**

- `$(wildcard)`：获取所有符合条件的文件路径。
- `$(patsubst)`：将源文件路径替换为目标文件路径。

### **完整示例**

假设目录结构如下：

```
src/
  main.cpp
  utils.cpp
  helper.c

```

Makefile 处理结果：

```makefile
CXX_SOURCES = src/main.cpp src/utils.cpp
C_SOURCES = src/helper.c
CXX_OBJECTS = build/main.o build/utils.o
C_OBJECTS = build/helper.o

```

这些变量可以用于规则中，自动生成目标文件的编译规则。