
![powerup22](https://user-images.githubusercontent.com/752380/142743460-5827b232-f0ec-4240-9eaa-0947fcc3a87c.png)

[![.NET](https://github.com/badamczewski/PowerUp/actions/workflows/dotnet.yml/badge.svg)](https://github.com/badamczewski/PowerUp/actions/workflows/dotnet.yml)

### **PowerUp** is a collection of productivity utilities, disassembly and decompilation tools for multiple languages and platforms.

The project features the following utilities and tools:

* Live IDE Watcher (For C#, F#, GO and Rust).
* .NET JIT Dissasembler.
* .NET IL Compiler.
* .NET Console with rich formatting.
* Others.

## Live IDE Watcher

A watcher application that monitors source code files and IR, IL files and compiles them and later decompiles and disassembles them to produce IL,IR and X86 ASM outputs. All compilers support multiple features such as Jump Guides, X86, IR Assembly documentation, Source Maps and more.

### Running

To run the application, you need to compile Power.Up watcher and run it from the terminal by providing the correct compiler(s) and providing input and output files like so:

```
.\PowerUp.Watcher.exe -rs D:\01_BA\PowerUp\_code.rs D:\01_BA\PowerUp\_outRust.asm
```

The application supports running multiple compilers at the same time:

```
.\PowerUp.Watcher.exe -rs D:\01_BA\PowerUp\_code.rs D:\01_BA\PowerUp\_outRust.asm -go D:\01_BA\PowerUp\_code.go D:\01_BA\PowerUp\_outGO.asm -cs D:\01_BA\PowerUp\_code.cs D:\01_BA\PowerUp\_out6.asm D:\01_BA\PowerUp\_out6.il
```

![obraz](https://user-images.githubusercontent.com/752380/142760629-f0d84b83-5357-40b4-8b2b-f221aca1bb99.png)


### C# Decompilation and dissasembly

C# is the only language that supports (at the moment) running code, interactive mode, benchmarking and class and struct layouts.

![power_up_cs_1](https://user-images.githubusercontent.com/752380/142741796-883cc8ac-259e-4e7b-9c76-624b8e3b7370.gif)

This demo shows the layouts feature:

![power_up_cs_2](https://user-images.githubusercontent.com/752380/142742770-ee02faca-f1f9-448c-9e70-f635a147f671.gif)

C# supports multiple attributes and comment-level attributes that can be used to control compilation:

```
[Bench]       <- Used on a method to Benchmak source code, the method needs to have no input arguments.
[Run]         <- Used on a method to Run source code, the method needs to have no input arguments.
Print(X)      <- This is a C# function that is used to print values when the code uses the Run attribuute
[ShowGuides]  <- Used on Any to enable jump guides in the ASM outputs.
[ShowASMDocs] <- Used on Any to turn on ASM code documentation.
[ShowASMDocs(offset={X}) <- Used on Any to turn on ASM code documentation. The offset argument controls the offset from ASM code where the docs are rendered.
[ShortAddr]   <- Used on Any to have short address lines in the output ASM code.
[ShortAddr(by={X})] <- Used on Any to have short address lines in the output ASM code. The additional argument is used to control the cut level. 
//up:showCode         <- Show source code maps, that map assembly instructions to source code.
//up:showGuides       <- Used to enable jump guides in the ASM outputs.
//up:showASMDocs      <- Used to turn on ASM code documentation.
//up:showASMDocs offset = {X | auto} <- Used to enable jump guides in the ASM outputs. The offset argument decides the position of the documentation.
//up:simpleNames      <- Simplify compiler generated names.
//up:showCode         <- Show source code maps, that map assembly instructions to source code.
//up:relativeAddr     <- All instruction adresses will start from zero.
//up:diff source={X}, target={Y} <- Creates a side by side diff of methods that are provided in the 'source' and 'target' parameters.
```

Due to some limitations with C# attributes certain features will remain exclusively as comment-level attributes.

### F# Decompilation and dissasembly

F# curently supports much of the features of the C# Watcher, the only thing that is missing is Running and Benchmarking code.

![obraz](https://user-images.githubusercontent.com/752380/152641753-28490801-e8b1-42d2-aed7-2f050c3d0e1a.png)

F# supports multiple comment-level attributes that can be used to control compilation:

```
//up:showCode         <- Show source code maps, that map assembly instructions to source code.
//up:showGuides       <- Used to enable jump guides in the ASM outputs.
//up:showASMDocs      <- Used to turn on ASM code documentation.
//up:showASMDocs offset = {X | auto} <- Used to enable jump guides in the ASM outputs. The offset argument decides the position of the documentation.
//up:simpleNames      <- Simplify compiler generated names.
//up:showCode         <- Show source code maps, that map assembly instructions to source code.
//up:relativeAddr     <- All instruction adresses will start from zero.
//up:diff source={X}, target={Y} <- Creates a side by side diff of methods that are provided in the 'source' and 'target' parameters.
```

### GO Decompilation

GO Lang is not disassembled to X86 asm, but GO-specific IR is almost a 1-to-1 assembly, so most optimizations have already happened. This makes this type of IR format viable for performance analysis.

![power_up_go_1](https://user-images.githubusercontent.com/752380/142741977-dd8e038a-c6a1-425a-bb07-5241762dfd14.gif)

GO supports multiple comment-level attributes that can be used to control compilation:

```
//up:showGuides       <- Used to enable jump guides in the ASM outputs.
//up:showASMDocs      <- Used to turn on ASM code documentation.
//up:showASMDocs offset = {X | auto} <- Used to enable jump guides in the ASM outputs. The offset argument decides the position of the documentation.
//up:showCode         <- Show source code maps, that map assembly instructions to source code.
//up:diff source={X}, target={Y} <- Creates a side by side diff of methods that are provided in the 'source' and 'target' parameters.
```

### Rust Dissasembly

Rust being a LLVM based language will support default compiler flags like optimization levels and source code maps. (This feature will be also added to c# and GO with time)

![power_up_rs_1](https://user-images.githubusercontent.com/752380/142742163-5c4907ad-754c-41b0-bc40-e8ad05288aa2.gif)

Rust supports multiple comment-level attributes that can be used to control compilation:

```
//up:showGuides       <- Used to enable jump guides in the ASM outputs.
//up:showASMDocs      <- Used to turn on ASM code documentation.
//up:showASMDocs offset = {X | auto} <- Used to enable jump guides in the ASM outputs. The offset argument decides the position of the documentation.
//up:optimization level = {X} <- Set the compilation optimization level (-C opt-level)
//up:showCode         <- Show source code maps, that map assembly instructions to source code.
//up:diff source={X}, target={Y} <- Creates a side by side diff of methods that are provided in the 'source' and 'target' parameters.
```

### .NET IL Compilation

Note: IL Compilation is still a work in progress, and it will take some time before it's robust.

![anim10](https://user-images.githubusercontent.com/752380/131910137-70f0ee68-b4fa-4bf3-b727-1a4ddaf86384.gif)

**I use this application daily to create infographics:** https://leveluppp.ghost.io/infographics/

If you would like to see more features, there's a Youtube video showing more features in detail:

https://www.youtube.com/watch?v=EZV_9sCrptc

### Look and Feel

To make your outputs look nice in Visual Studio Code or any other editor, you must install an X86 assembly syntax.

I use a modified version of the 13xforever X86 ASM syntax: https://github.com/13xforever/x86-assembly-textmate-bundle
This version is bundled with the project and can be found here:

https://github.com/badamczewski/PowerUp/tree/main/external/13xforever.language-x86-64-assembly-3.0.0

Additionally you will need *Cascadia Mono* for nice guides and other features.

## .NET JIT Dissasembler

To disassemble JIT code, you need to extract the method info using reflection and call the extension method ToAsm(). This will get native assembly code in tier0. To get a higher Tier, you need to provide the delegate that will call the method, and over time the compiler will re-JIT it to Tier1. If you want to skip this, you can compile your project with:  

```<TieredCompilation>false</TieredCompilation>```

Example:

```csharp

   typeof(Program)
       .GetMethod("DecompilationTestMethod")
       .ToAsm()
       .Print();
```

Example for Tier1:

```csharp

    typeof(Program)
        .GetMethod("DecompilationTestMethod")
        .ToAsm(() => p.DecompilationTestMethod(10))
        .tier1
        .Print();
```

There are no guarantees that Tier1 will always be available; Very short and fast methods tend not to be promoted (I'm working on a fix). Code that contains loops is always optimized so you should not bother with this method and switch back to the simpler version.

## .NET IL Compiler 

You can write IL Code as a string and compile it to a type; later, it can be fed to the JIT Decompiler. Native IL compilation is an interesting research topic since you can emit instructions that are not used or used in a completely different context.

```csharp
   var il = @"
    .method public hidebysig instance int32 X (int32 x) 
    {
       .maxstack 8

       IL_0000: ldarg.1
       IL_0001: ldc.i4.s 97
       IL_0003: callvirt instance int32 [System.Private.CoreLib]System.String::IndexOf(char)
       IL_0008: ret
    }
   "; 
   ILCompiler compiler = new ILCompiler();
   var type = compiler.Compile(il);
   var asm = type.CompiledType.ToAsm();
   asm.Print();
```

## Open Source

This project uses many open source projects, like:

- ICsharpCodeDecompiler
- BenchmarkDotNet
- Microsoft Roslyn Compiler Stack 

Additionally, some of the projects were pulled into PowerUp source code and modified:

- X86 ASSEMBLY Visual Studio Code Template: https://github.com/13xforever/x86-assembly-textmate-bundle

```
The template was altered to support custom elements, like jump guides and numerous 'special' keywords and instructions.
```

- DiffPlex Diff: https://github.com/mmanela/diffplex

```
The project is pulled into PowerUp source code as is, but WPF, Web and WinForm projects were removed since PowerUp just needs to be able to do diffs without any
UI Dependencies.
```
