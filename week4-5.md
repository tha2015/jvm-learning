# Week 4-5: Memory Management & Garbage Collection

## Learning Objectives
By the end of these 2 weeks, you will:
- [ ] Understand JVM memory layout (heap generations, metaspace, direct memory)
- [ ] Compare and analyze different GC algorithms (G1, ZGC, Shenandoah, Parallel)
- [ ] Use advanced memory analysis tools to diagnose memory issues
- [ ] Optimize GC performance for different application patterns
- [ ] Identify and resolve memory leaks using profiling tools

## Time Allocation (30 hours total)
- **Reading/Study**: 12 hours (40%)
- **Hands-on Practice**: 10.5 hours (35%)
- **Projects**: 7.5 hours (25%)

## Week 4: Memory Structure & GC Fundamentals

### Learning Materials
**Books:**
- *Java Performance* by Scott Oaks - Chapter 5: "Garbage Collection" (3 hours)
- *Java Performance* by Scott Oaks - Chapter 6: "Garbage Collection Algorithms" (3 hours)

**Online Course:**
- [Java Memory Management](https://www.udemy.com/course/java-application-performance-and-memory-management/) by Matt Greencroft - Sections 1-4 (4 hours)

**Specifications & Documentation:**
- [HotSpot Memory Management](https://docs.oracle.com/en/java/javase/21/gctuning/) - Oracle GC Tuning Guide (2 hours)
- [OpenJDK GC Documentation](https://wiki.openjdk.org/display/HotSpot/Main) (1 hour)

### Hands-on Activities
1. **Memory Layout Exploration** (3 hours)
   ```bash
   # Analyze heap structure with different GC algorithms
   java -XX:+UseG1GC -XX:+PrintGCDetails YourApp
   java -XX:+UseZGC -XX:+PrintGCDetails YourApp
   java -XX:+UseParallelGC -XX:+PrintGCDetails YourApp

   # Use jstat for real-time memory monitoring
   jstat -gc -t <pid> 5s
   jstat -gccapacity <pid>
   ```

2. **GC Behavior Analysis** (2.5 hours)
   - Create applications with different allocation patterns
   - Monitor GC behavior with JFR: `java -XX:+FlightRecorder -XX:StartFlightRecording=duration=60s,filename=gc-analysis.jfr`
   - Use VisualVM to visualize heap usage patterns

### Projects
**Project 1: Memory Allocation Pattern Analyzer** (4 hours)
```java
// Goal: Build a tool that creates different allocation patterns and measures GC impact
public class AllocationPatternAnalyzer {
    // Test scenarios:
    // - Short-lived objects (young gen pressure)
    // - Long-lived objects (old gen impact)
    // - Large objects (humongous objects in G1)
    // - Mixed allocation patterns
}
```
**Deliverables:**
- Benchmark suite with different allocation patterns
- GC performance comparison report (G1 vs ZGC vs Parallel)
- Recommendations for pattern-specific GC tuning

**Success Criteria:**
- [ ] Accurately measures GC overhead for each pattern
- [ ] Provides clear performance comparisons
- [ ] Includes memory efficiency metrics

## Week 5: Advanced Memory Analysis & Leak Detection

### Learning Materials
**Books:**
- Complete [Java Memory Management Course](https://www.udemy.com/course/java-application-performance-and-memory-management/) - Sections 5-8 (4 hours)

**Documentation:**
- [Eclipse MAT Documentation](https://www.eclipse.org/mat/documentation/) - Memory Analysis Guide (2 hours)
- [GCeasy.io Analysis Guide](https://gceasy.io/gc-recommendations.jsp) (1 hour)

**Advanced Resources:**
- [Memory Leaks Detection Best Practices](https://www.baeldung.com/java-memory-leaks) (1 hour)
- [Direct Memory and Off-Heap Usage](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/memleaks002.html) (1 hour)

### Hands-on Activities
1. **Memory Leak Simulation & Detection** (3 hours)
   ```java
   // Create intentional memory leaks for practice:
   // - Static collection growth
   // - Listener registration without cleanup
   // - ThreadLocal leaks
   // - ClassLoader leaks
   ```
   - Use Eclipse MAT to analyze heap dumps
   - Practice with `jmap -dump:format=b,file=heap.hprof <pid>`

2. **Advanced Memory Tools** (2.5 hours)
   - Use JProfiler for memory profiling
   - Analyze direct memory usage with `-XX:NativeMemoryTracking=summary`
   - Practice with GCeasy.io for GC log analysis

### Projects
**Project 2: Memory Leak Detective Tool** (3.5 hours)
```java
// Goal: Automated tool for memory leak detection and analysis
public class MemoryLeakDetective {
    // Features:
    // - Automated heap dump analysis
    // - Leak pattern recognition
    // - Trend analysis over time
    // - Report generation with recommendations
}
```
**Deliverables:**
- CLI tool that processes heap dumps
- Automated leak detection algorithms
- HTML report with visualizations and recommendations
- Integration with common CI/CD pipelines

**Success Criteria:**
- [ ] Detects common leak patterns automatically
- [ ] Provides actionable remediation suggestions
- [ ] Handles large heap dumps efficiently (>4GB)

## Advanced Topics & Experiments

### GC Algorithm Deep Dive
**G1 Garbage Collector:**
```bash
# Key G1 flags for experimentation
-XX:+UseG1GC
-XX:G1HeapRegionSize=16m
-XX:MaxGCPauseMillis=200
-XX:G1NewSizePercent=30
-XX:G1MaxNewSizePercent=40
```

**ZGC (Low-Latency Collector):**
```bash
# ZGC flags for ultra-low latency
-XX:+UseZGC
-XX:+UseLargePages
-XX:+UnlockExperimentalVMOptions
```

**Shenandoah GC:**
```bash
# Shenandoah for consistent low pause times
-XX:+UseShenandoahGC
-XX:+UnlockExperimentalVMOptions
-XX:ShenandoahGCHeuristics=compact
```

### Memory Tuning Experiments
1. **Heap Sizing Impact** (1 hour)
   - Test applications with different `-Xms` and `-Xmx` settings
   - Measure startup time vs. steady-state performance trade-offs

2. **Off-Heap Memory Usage** (1 hour)
   - Experiment with direct ByteBuffers
   - Use libraries like Chronicle Map for off-heap storage
   - Monitor with `-XX:NativeMemoryTracking=detail`

## Weekly Checkpoints

### Week 4 Checkpoint
- [ ] Can explain heap generations and memory areas
- [ ] Successfully compared GC algorithms with benchmarks
- [ ] Comfortable interpreting GC logs and JFR recordings

### Week 5 Checkpoint
- [ ] Can identify and resolve memory leaks using MAT
- [ ] Built working memory analysis automation
- [ ] Understands direct memory and off-heap implications

## Essential Tools Configuration

### Eclipse MAT Setup
```bash
# Download and configure Eclipse MAT
# Increase memory for large heap analysis
-vmargs -Xmx8g
```

### JFR Configuration for Memory Analysis
```bash
# Comprehensive memory profiling settings
java -XX:+FlightRecorder \
     -XX:StartFlightRecording=duration=300s,filename=memory-profile.jfr,settings=profile \
     YourApplication
```

### VisualVM Memory Profiling
- Configure sampling vs. profiling modes
- Set up remote JMX connections
- Create custom MBeans for application metrics

## Performance Benchmarking

### JMH Memory Benchmarks
```java
@Benchmark
@BenchmarkMode(Mode.AverageTime)
@OutputTimeUnit(TimeUnit.NANOSECONDS)
@Measurement(iterations = 5, time = 10, timeUnit = TimeUnit.SECONDS)
public void testAllocationPattern() {
    // Benchmark different allocation strategies
}
```

## Troubleshooting Guide

### Common Memory Issues
1. **OutOfMemoryError: Java heap space**
   - Check for memory leaks with MAT
   - Analyze heap dump for large object retention
   - Review GC efficiency metrics

2. **OutOfMemoryError: Metaspace**
   - Monitor class loading and unloading
   - Check for ClassLoader leaks
   - Adjust `-XX:MetaspaceSize` if needed

3. **GC Overhead Limit Exceeded**
   - Analyze GC efficiency with GCeasy
   - Consider different GC algorithm
   - Review application allocation patterns

### Performance Optimization Checklist
- [ ] GC pause times within acceptable limits
- [ ] Memory utilization efficiency >80%
- [ ] No detected memory leaks
- [ ] Appropriate heap sizing for workload

## Next Week Preview
Week 6-7 will focus on JIT compilation and performance optimization, building on the memory management foundation established in these weeks.