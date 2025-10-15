# Week 6-7: JIT Compilation & Benchmarking

## Learning Objectives
By the end of these 2 weeks, you will:
- [ ] Understand C1 (Client) and C2 (Server) compiler architectures and optimization techniques
- [ ] Master JMH (Java Microbenchmark Harness) for accurate performance measurement
- [ ] Use JITWatch to analyze JIT compilation decisions and optimizations
- [ ] Interpret JIT compilation logs and identify performance bottlenecks
- [ ] Apply advanced JIT tuning techniques for optimal performance

## Time Allocation (30 hours total)
- **Reading/Study**: 12 hours (40%)
- **Hands-on Practice**: 10.5 hours (35%)
- **Projects**: 7.5 hours (25%)

## Week 6: JIT Compiler Architecture & Optimization

### Learning Materials
**Books:**
- *Optimizing Java* by Benjamin J. Evans, James Gough, Chris Newland - Chapter 3: "Hardware and Operating Systems" (2 hours)
- *Optimizing Java* - Chapter 4: "Performance Testing Patterns and Antipatterns" (2 hours)

**Online Resources:**
- [HotSpot Compiler Architecture](https://wiki.openjdk.org/display/HotSpot/Compiler) - OpenJDK Wiki (2 hours)
- [JIT Compilation in HotSpot](https://www.oracle.com/technical-resources/articles/java/architect-evans-pt1.html) (1 hour)
- [Understanding JIT Optimizations](https://shipilev.net/jvm/anatomy-quarks/) - Aleksey Shipilёv's articles on inlining, escape analysis (2 hours)

**Research Papers:**
- [Adaptive Optimization in the Jalapeño JVM](https://www.research.ibm.com/people/d/dgrove/papers/oopsla00.pdf) (1 hour)

**Video Resources:**
- [OpenJDK: HotSpot Intrinsics](https://www.youtube.com/watch?v=e9EfIOSL6ZY) - Understanding intrinsic methods (1 hour)
- [JIT Compilation Deep Dive](https://www.youtube.com/watch?v=r_hxJkn1bMI) - Oracle Code One presentations (1 hour)

### Hands-on Activities
1. **JIT Compilation Analysis** (3 hours)
   ```bash
   # Enable detailed JIT logging
   java -XX:+PrintCompilation \
        -XX:+UnlockDiagnosticVMOptions \
        -XX:+PrintInlining \
        -XX:+PrintCodeCache \
        -XX:+DebugNonSafepoints \
        YourApplication

   # Advanced JIT analysis flags
   java -XX:+UnlockDiagnosticVMOptions \
        -XX:+TraceClassLoading \
        -XX:+LogVMOutput \
        -XX:LogFile=jit-analysis.log \
        YourApplication
   ```

2. **JITWatch Exploration** (2.5 hours)
   - Download and setup [JITWatch](https://github.com/AdoptOpenJDK/jitwatch)
   - Analyze method inlining decisions
   - Study deoptimization events
   - Examine assembly code generation

### Projects
**Project 1: JIT Performance Analyzer** (4 hours)
```java
// Goal: Build a comprehensive JIT analysis tool
public class JITPerformanceAnalyzer {
    // Features:
    // - Parse JIT compilation logs
    // - Identify hot methods and inlining opportunities
    // - Detect deoptimization patterns
    // - Generate performance recommendations
    // - Create visualizations of compilation activity
}
```

**Deliverables:**
- Log parser that extracts JIT compilation statistics
- Interactive HTML report showing compilation timeline
- Method hotness ranking with optimization suggestions
- Deoptimization analysis and mitigation recommendations

**Success Criteria:**
- [ ] Accurately parses complex JIT logs
- [ ] Identifies top optimization opportunities
- [ ] Provides actionable performance insights
- [ ] Handles large applications (1000+ classes)

## Week 7: JMH Benchmarking & Performance Testing

### Learning Materials
**Documentation:**
- [JMH Official Samples](http://hg.openjdk.java.net/code-tools/jmh/file/tip/jmh-samples/src/main/java/org/openjdk/jmh/samples/) - Study samples 1-20 (3 hours)
- [JMH User Guide](https://github.com/openjdk/jmh/blob/master/jmh-core/src/main/java/org/openjdk/jmh/annotations/package-info.java) (2 hours)

**Articles:**
- [JMH Best Practices](https://www.baeldung.com/java-microbenchmark-harness) (1 hour)
- [Avoiding Benchmarking Pitfalls](https://shipilev.net/talks/joker-Oct2014-benchmarking.pdf) - Aleksey Shipilёv's presentation (1 hour)
- [Statistical Analysis of JMH Results](https://stackoverflow.com/questions/504103/how-do-i-write-a-correct-micro-benchmark-in-java) (1 hour)

**Video Resources:**
- [JMH Deep Dive](https://www.youtube.com/watch?v=VaWgOCDBxYw) - Devoxx presentation (1 hour)

### Hands-on Activities
1. **JMH Benchmark Development** (3 hours)
   ```java
   @BenchmarkMode(Mode.AverageTime)
   @OutputTimeUnit(TimeUnit.NANOSECONDS)
   @State(Scope.Thread)
   @Warmup(iterations = 5, time = 10, timeUnit = TimeUnit.SECONDS)
   @Measurement(iterations = 5, time = 10, timeUnit = TimeUnit.SECONDS)
   @Fork(1)
   public class DataStructureBenchmarks {
       // Benchmark ArrayList vs LinkedList operations
       // Compare different Map implementations
       // Test string concatenation methods
   }
   ```

2. **Advanced JMH Features** (2.5 hours)
   - Use `@State` scopes effectively
   - Implement custom profilers
   - Practice with `Blackhole.consume()` and `@CompilerControl`
   - Analyze JMH result statistics

### Projects
**Project 2: Performance Regression Test Suite** (3.5 hours)
```java
// Goal: Automated performance regression detection system
public class PerformanceRegressionSuite {
    // Features:
    // - Baseline performance establishment
    // - Automated regression detection
    // - Statistical significance testing
    // - CI/CD integration capabilities
    // - Performance trend analysis
}
```

**Deliverables:**
- JMH-based benchmark suite for core application functions
- Automated regression detection with configurable thresholds
- Integration with build pipelines (Maven/Gradle plugins)
- Performance dashboard with historical trends
- Alert system for significant performance changes

**Success Criteria:**
- [ ] Detects 5% performance regressions reliably
- [ ] Minimizes false positives through statistical analysis
- [ ] Integrates seamlessly with CI/CD workflows
- [ ] Provides clear performance trending visualizations

## Advanced JIT Optimization Techniques

### Escape Analysis Deep Dive
```java
// Understanding escape analysis impact
public class EscapeAnalysisDemo {
    // Test scenarios:
    // - Stack allocation vs heap allocation
    // - Lock elision opportunities
    // - Scalar replacement effects

    @Benchmark
    public int stackAllocation() {
        Point p = new Point(1, 2); // May be stack allocated
        return p.x + p.y;
    }

    @Benchmark
    public Point heapAllocation() {
        Point p = new Point(1, 2); // Must be heap allocated
        return p; // Escapes method
    }
}
```

### Inlining Analysis
```bash
# Analyze inlining decisions
java -XX:+PrintInlining \
     -XX:+UnlockDiagnosticVMOptions \
     -XX:InlineSmallCode=1000 \
     -XX:MaxInlineLevel=15 \
     YourBenchmark
```

### Loop Optimizations
```java
// Study vectorization and loop unrolling
@Benchmark
public void vectorizationCandidate(int[] array) {
    for (int i = 0; i < array.length; i++) {
        array[i] = array[i] * 2 + 1; // Vectorizable operation
    }
}
```

## Performance Analysis Methodology

### Benchmark Design Principles
1. **Isolation**: Test one thing at a time
2. **Repeatability**: Consistent measurement conditions
3. **Relevance**: Representative of real workload
4. **Statistical Significance**: Adequate sample sizes

### JMH Best Practices Checklist
- [ ] Use appropriate `@BenchmarkMode`
- [ ] Configure sufficient warmup iterations
- [ ] Handle dead code elimination with `Blackhole`
- [ ] Use `@State` to manage benchmark data
- [ ] Fork JVMs to avoid profile pollution
- [ ] Analyze result distributions, not just averages

## Weekly Checkpoints

### Week 6 Checkpoint
- [ ] Can interpret JIT compilation logs effectively
- [ ] Understands major JIT optimizations (inlining, escape analysis)
- [ ] Successfully used JITWatch for method analysis
- [ ] Built working JIT performance analysis tool

### Week 7 Checkpoint
- [ ] Masters JMH for accurate microbenchmarking
- [ ] Can design statistically valid performance tests
- [ ] Built automated performance regression detection
- [ ] Understands common benchmarking pitfalls and how to avoid them

## Tool Setup & Configuration

### JITWatch Installation
```bash
# Download from GitHub
git clone https://github.com/AdoptOpenJDK/jitwatch.git
cd jitwatch
mvn clean compile exec:java
```

### JMH Project Setup
```xml
<!-- Maven dependency for JMH -->
<dependency>
    <groupId>org.openjdk.jmh</groupId>
    <artifactId>jmh-core</artifactId>
    <version>1.37</version>
</dependency>
<dependency>
    <groupId>org.openjdk.jmh</groupId>
    <artifactId>jmh-generator-annprocess</artifactId>
    <version>1.37</version>
    <scope>provided</scope>
</dependency>
```

### Profiler Integration
```java
// Enable built-in profilers
@Fork(value = 1, jvmArgs = {"-prof", "gc"})      // GC profiler
@Fork(value = 1, jvmArgs = {"-prof", "comp"})    // Compiler profiler
@Fork(value = 1, jvmArgs = {"-prof", "stack"})   // Stack profiler
public class ProfiledBenchmark {
    // Your benchmarks here
}
```

## Common JIT Optimization Patterns

### Method Inlining Opportunities
- Small, frequently called methods
- Interface calls with single implementation
- Virtual calls with predictable targets

### Escape Analysis Benefits
- Stack allocation of short-lived objects
- Lock elision for uncontended synchronization
- Scalar replacement of object fields

### Loop Optimizations
- Vectorization of arithmetic operations
- Loop unrolling for better ILP
- Range check elimination

## Troubleshooting Performance Issues

### JIT Compilation Problems
1. **Method not compiling**: Check invocation thresholds
2. **Deoptimization cycles**: Analyze profile pollution
3. **Code cache exhaustion**: Monitor with `-XX:+PrintCodeCache`

### Benchmarking Antipatterns
1. **Dead code elimination**: Use `Blackhole.consume()`
2. **Constant folding**: Avoid compile-time constants
3. **Loop optimizations**: Be aware of JIT loop analysis

## Next Week Preview
Week 8-9 will focus on advanced profiling and native memory tracking, building on the JIT optimization knowledge from these weeks.