# REPL调研--Swift REPL模式



### Swift

#### 技术路线

在IR层面支持REPL，提供swift解释器，swift提供了编译器runtime，提供基础的词法分析、语法分析、IR生成能力，并可基于llvm ir进行表达式eval，通过JIT的方式在解释器中支持REPL。

#### 源码分析

1. 头文件：`include/swift/Immediate/Immediate.h`，包含两个接口

   ```cpp
   int RunImmediately(CompilerInstance &CI, const ProcessCmdLine &CmdLine,
                        const IRGenOptions &IRGenOpts, const SILOptions &SILOpts,
                        std::unique_ptr<SILModule> &&SM);
   void runREPL(CompilerInstance &CI, const ProcessCmdLine &CmdLine,
                  bool ParseStdlib);
   ```

   - RunImmediately方法用于基于**SIL（Swift Intermediate Language）**，立即Eval当前IR Module，相当于是解释器
   - runREPL方法提供给FrontendTool.cpp前端逻辑进行调用，作为REPL的main loop

2. 源码文件：Immediate.cpp

实现几个功能：

```cpp
void *loadSwiftRuntime(ArrayRef<std::string> runtimeLibPaths);
bool tryLoadLibraries(ArrayRef<LinkLibrary> LinkLibraries,
                      SearchPathOptions SearchPathOpts,
                      DiagnosticEngine &Diags);
bool linkLLVMModules(llvm::Module *Module,
                     std::unique_ptr<llvm::Module> SubModule);
bool autolinkImportedModules(ModuleDecl *M, const IRGenOptions &IRGenOpts);
int swift::RunImmediately(CompilerInstance &CI,
                          const ProcessCmdLine &CmdLine,
                          const IRGenOptions &IRGenOpts,
                          const SILOptions &SILOpts,
                          std::unique_ptr<SILModule> &&SM);
```

- 加载swift编译器runtime：swiftCore
- llvm ir module间合并
- import module的支持
- RunImmediately：将input翻译成llvm ir，调用`llvm::ExecutionEngine`直接执行llvm ir

3. 源码文件：REPL.cpp

REPL的主函数，从Frontend.cpp进来，主要由一个读取用户input的main loop，对每个输入进行处理。依赖histedit的支持

#### Reference:

[Source Code Immediate.cpp](https://github.com/apple/swift/blob/master/lib/Immediate/Immediate.cpp)

[Source Code REPL.cpp](https://github.com/apple/swift/blob/master/lib/Immediate/REPL.cpp)

[histedit.h: Line editor and history interface.]()