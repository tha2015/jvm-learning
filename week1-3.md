# Week 1-3: JVM Architecture & Bytecode

## Learning Objectives
By the end of these 3 weeks, you will:
- [ ] Understand JVM memory structure (heap, stack, method area, PC register)
- [ ] Explain the class loading process and custom ClassLoader implementation
- [ ] Read and interpret Java bytecode using various tools
- [ ] Debug class loading issues using JVM debugging tools
- [ ] Understand JVM startup sequence and bootstrap class loading

## Time Allocation (45 hours total)
- **Reading/Study**: 18 hours (40%)
- **Hands-on Practice**: 16 hours (35%)
- **Projects**: 11 hours (25%)

## Week 1: JVM Structure & Class Loading

### Learning Materials
**Books:**
- *Java Performance* by Scott Oaks - Chapter 1: "Introduction" (2 hours)
- *Java Performance* by Scott Oaks - Chapter 2: "An Approach to Performance Testing" (2 hours)

**Specifications:**
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 2: "The Structure of the Java Virtual Machine" (3 hours)
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 5: "Loading, Linking, and Initializing" (2 hours)

**Online Resources:**
- [Oracle JVM Internals Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/) (1 hour)
- [Baeldung: Understanding JVM Internals](https://www.baeldung.com/jvm-internals) (30 min)

### Hands-on Activities
1. **JVM Structure Exploration** (2 hours)
   - Use `jcmd <pid> VM.classloader_stats` to see class loading statistics
   - Use `jmap -histo <pid>` to analyze heap object distribution
   - Use `jstack <pid>` to examine thread stacks

2. **Class Loading Investigation** (3 hours)
   - Create a simple Java program and trace class loading with `-verbose:class`
   - Experiment with different classpath configurations
   - Use `jdb` to set breakpoints in class loading process

### Projects
**Project 1: Custom ClassLoader for Encrypted Classes** (4 hours)
```java
// Goal: Build a ClassLoader that can load encrypted .class files
public class EncryptedClassLoader extends ClassLoader {
    // Implement decryption logic and class loading
}
```
**Deliverables:**
- Working EncryptedClassLoader implementation
- Test encrypted class files
- Documentation of loading process

**Success Criteria:**
- [ ] Can load and execute encrypted classes
- [ ] Proper parent delegation handling
- [ ] Error handling for corrupt/invalid files

## Week 2: Bytecode Analysis & Tools

### Learning Materials
**Books:**
- *Java Performance* by Scott Oaks - Continue Chapter 2 (1 hour)

**Specifications:**
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 3: "Compiling for the Java Virtual Machine" (2 hours)
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 4: "The class File Format" (3 hours)

**Online Resources:**
- [Oracle Bytecode Tutorial](https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-6.html) (2 hours)
- [ASM Bytecode Framework Guide](https://asm.ow2.io/asm4-guide.pdf) - Chapters 1-2 (2 hours)

### Hands-on Activities
1. **Bytecode Inspection** (3 hours)
   - Use `javap -c -v` on various Java constructs (loops, conditionals, method calls)
   - Compare bytecode between different Java versions
   - Install and use IntelliJ Bytecode Viewer plugin

2. **Bytecode Modification** (2 hours)
   - Use ASM library to modify method behavior
   - Create simple bytecode instrumentation

### Projects
**Project 2: Bytecode Analysis Tool** (4 hours)
```java
// Goal: Build a tool that analyzes complexity metrics from bytecode
public class BytecodeAnalyzer {
    // Parse .class files and extract metrics
    // - Method complexity (instruction count)
    // - Dependency analysis
    // - Performance hints
}
```
**Deliverables:**
- CLI tool that accepts .class files
- Reports on method complexity and potential optimizations
- Comparison reports between similar methods

**Success Criteria:**
- [ ] Correctly parses standard .class files
- [ ] Provides meaningful complexity metrics
- [ ] Handles edge cases (abstract methods, native methods)

## Week 3: JVM Startup & Advanced Class Loading

### Learning Materials
**Books:**
- Review *Java Performance* Chapters 1-2 (1 hour)

**OpenJDK Source Code:**
- Explore `src/hotspot/share/classfile/` directory (2 hours)
- Study `systemDictionary.cpp` and `classLoader.cpp` (2 hours)

**Online Resources:**
- [OpenJDK Wiki: HotSpot Glossary](https://wiki.openjdk.org/display/HotSpot/Glossary) (1 hour)
- [JVM Startup Process Deep Dive](https://shipilev.net/jvm/anatomy-quarks/) - Relevant articles (2 hours)

### Hands-on Activities
1. **JVM Startup Analysis** (3 hours)
   - Use `-XX:+TraceClassLoading` to see bootstrap loading
   - Analyze startup time with different JVM flags
   - Use JFR to profile JVM startup: `java -XX:+FlightRecorder -XX:StartFlightRecording=duration=10s,filename=startup.jfr`

2. **Advanced ClassLoader Scenarios** (2 hours)
   - Implement parent-last class loading
   - Handle class loading deadlocks
   - Test with multiple class loaders

### Projects
**Project 3: JVM Startup Profiler** (4 hours)
```java
// Goal: Tool to analyze and optimize JVM startup performance
public class StartupProfiler {
    // Measure and report:
    // - Class loading time breakdown
    // - JIT compilation during startup
    // - Memory allocation patterns
    // - Suggestions for optimization
}
```
**Deliverables:**
- Startup analysis tool with JFR integration
- Report template showing optimization opportunities
- Before/after comparison capabilities

**Success Criteria:**
- [ ] Accurately measures startup phases
- [ ] Provides actionable optimization suggestions
- [ ] Works with different application types

## Weekly Checkpoints

### Week 1 Checkpoint
- [ ] Can explain JVM memory areas and their purposes
- [ ] Successfully implemented custom ClassLoader
- [ ] Comfortable using basic JVM diagnostic tools

### Week 2 Checkpoint
- [ ] Can read and interpret bytecode for common Java constructs
- [ ] Built working bytecode analysis tool
- [ ] Understands relationship between Java source and bytecode

### Week 3 Checkpoint
- [ ] Understands JVM startup sequence in detail
- [ ] Can optimize application startup using profiling data
- [ ] Comfortable exploring OpenJDK source code

## Tools Setup
Ensure you have these tools installed and configured:
- **OpenJDK 21** with source code
- **IntelliJ IDEA** with bytecode viewer plugin
- **Eclipse MAT** for memory analysis
- **JProfiler or VisualVM** for profiling
- **ASM Framework** for bytecode manipulation

## Troubleshooting Common Issues
1. **ClassNotFoundException during custom loading**: Check parent delegation
2. **JVM crashes during debugging**: Use `-XX:+ShowMessageBoxOnError` for debugging
3. **Bytecode verification errors**: Ensure proper stack map frames

## Next Week Preview
Week 4-5 will focus on memory management and garbage collection, building on the JVM structure knowledge from these weeks.