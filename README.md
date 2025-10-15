# JVM Expert Master Plan (2025)

This plan guides you through mastering the JVM, with progress checkboxes to track your learning journey.

---

## Phase 1: Fundamentals (Weeks 1-4)

### Week 1-2: JVM Architecture & Bytecode
- [ ] Study JVM structure, class loading, and bytecode basics
- [ ] Read *Java Performance* by Scott Oaks, Chapters 1-2
- [ ] Review [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/), Chapters 2-5
- [ ] Use `javap -c -v` and IntelliJ Bytecode Viewer to inspect bytecode
- [ ] Build a custom ClassLoader for encrypted classes
- [ ] Explore OpenJDK source: `src/hotspot/share/classfile/`
- [ ] Debug class loading with `jdb` and breakpoints

### Week 3-4: Memory & Garbage Collection
- [ ] Learn heap layout and GC algorithms (G1, ZGC, Shenandoah)
- [ ] Read *Java Performance* Chapters 5-6
- [ ] Complete [Java Memory Management](https://www.udemy.com/course/java-application-performance-and-memory-management/) by Matt Greencroft
- [ ] Use Eclipse MAT, VisualVM, and GCeasy for heap analysis
- [ ] Analyze a memory leak and compare GC performance using tools

---

## Phase 2: Performance & Execution (Weeks 5-8)

### Week 5-6: JIT Compilation & Benchmarking
- [ ] Study C1/C2 compilers and optimization techniques
- [ ] Read *Optimizing Java* Chapters 3-4
- [ ] Use JMH and JITWatch to create and analyze benchmarks
- [ ] Analyze JIT compilation logs with JVM flags like `-XX:+PrintCompilation`

### Week 7-8: Advanced Profiling & Native Memory
- [ ] Learn off-heap memory and native memory tracking
- [ ] Practice profiling with async-profiler and Java Flight Recorder (JFR)
- [ ] Profile a real application and optimize hotspot methods

---

## Phase 3: Modern JVM Features (Weeks 9-12)

### Week 9-10: Virtual Threads & Structured Concurrency
- [ ] Study Project Loom: virtual threads and structured concurrency APIs
- [ ] Read JEP 444 and JEP 453 specifications
- [ ] Take Rock the JVM advanced Java modules
- [ ] Migrate thread-pool based app to virtual threads and measure performance

### Week 11-12: Production JVM & Container Tuning
- [ ] Learn container-aware JVM tuning and monitoring
- [ ] Use JMC, Arthas, Prometheus, Grafana for observability
- [ ] Setup JFR to Prometheus to Grafana monitoring pipeline
- [ ] Apply container JVM flags and tune for production

---

## Phase 4: Mastery & Capstone (Weeks 13-16)

### Week 13-14: GraalVM Native Image & AOT
- [ ] Learn GraalVM native image creation and limitations
- [ ] Review GraalVM documentation on native image metadata
- [ ] Build a native image for a Spring Boot app with <100ms startup

### Week 15-16: Capstone Project (choose one)
- [ ] Optimize an open-source Java app end-to-end using JVM profiling and tuning
- [ ] Build a custom JVM monitoring platform with alerting
- [ ] Migrate an existing app to virtual threads and benchmark improvements
- [ ] Deploy a production-ready GraalVM native image application

---

## Essential Tools & Resources
- Profiling: VisualVM, async-profiler, JProfiler  
- Monitoring: Java Flight Recorder (JFR), Java Mission Control (JMC), Arthas  
- Analysis: Eclipse MAT, JITWatch, GCeasy  
- Benchmarking: JMH, Gatling  
- Debugging: jdb, jstack, jmap, jcmd, gdb  

---

## Study Schedule
- 12-15 hours per week  
- Weekdays: 1.5-2 hours each  
- Weekends: 3-4 hours each  
- Suggested allocation: 40% reading/videos, 35% hands-on, 25% projects  

---

## Community & Continuous Learning
- Follow JVM Language Summit: https://openjdk.org/projects/mlvm/summit/  
- Join /r/java subreddit: https://www.reddit.com/r/java/  
- Join Java Discord: https://discord.gg/java  
- Subscribe to Inside Java newsletter  
- Practice with personal projects and open-source contributions  

---

*Progress through this checklist to build deep mastery of JVM internals, performance, and the latest JVM features in 2025.*

