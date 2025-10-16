# Week 1-3: JVM Architecture & Performance Instrumentation

## Learning Objectives
By the end of these 3 weeks, you will:
- [ ] Understand JVM memory structure (heap, stack, method area, PC register)
- [ ] Master ByteBuddy for runtime bytecode manipulation and instrumentation
- [ ] Build production-ready performance monitoring tools
- [ ] Analyze method performance and memory allocation patterns
- [ ] Understand JVM startup sequence and class loading internals

## Time Allocation (45 hours total)
- **Reading/Study**: 18 hours (40%)
- **Hands-on Practice**: 16 hours (35%)
- **Projects**: 11 hours (25%)

## Week 1: JVM Structure & ByteBuddy Foundation

### Learning Materials
**Books:**
- *Java Performance* by Scott Oaks - Chapter 1: "Introduction" (2 hours)
- *Java Performance* by Scott Oaks - Chapter 2: "An Approach to Performance Testing" (2 hours)

**Specifications:**
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 2: "The Structure of the Java Virtual Machine" (3 hours)
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 5: "Loading, Linking, and Initializing" (2 hours)

**ByteBuddy & Instrumentation:**
- [ByteBuddy Documentation](https://bytebuddy.net/#/tutorial) - Tutorial sections 1-3 (2 hours)
- [ByteBuddy GitHub Examples](https://github.com/raphw/byte-buddy/tree/master/byte-buddy-dep/src/test/java/net/bytebuddy) (1 hour)

**Online Resources:**
- [Oracle JVM Internals Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/) (1 hour)
- [Baeldung: JVM Architecture](https://www.baeldung.com/jvm-vs-jre-vs-jdk) (30 min)
- [JVM Internals Overview](https://blog.jamesdbloom.com/JVMInternals.html) (45 min)

### Hands-on Activities
1. **JVM Structure Exploration** (2 hours)
   - Use `jcmd <pid> VM.classloader_stats` to see class loading statistics
   - Use `jmap -histo <pid>` to analyze heap object distribution
   - Use `jstack <pid>` to examine thread stacks

2. **ByteBuddy Basic Instrumentation** (3 hours)
   ```java
   // Basic ByteBuddy instrumentation examples
   new ByteBuddy()
       .redefine(ExampleClass.class)
       .method(ElementMatchers.named("targetMethod"))
       .intercept(MethodDelegation.to(TimingInterceptor.class))
       .make()
       .load(ClassLoader.getSystemClassLoader());
   ```
   - Create simple method interceptors
   - Practice with ElementMatchers for method selection
   - Experiment with different interception strategies

### Projects
**Project 1: Core Performance Instrumentation Engine** (4 hours)
```java
// Goal: Build ByteBuddy-based performance instrumentation framework
public class PerformanceInstrumentationEngine {
    public void instrumentClass(String className, InstrumentationConfig config) {
        // Use ByteBuddy to instrument methods for performance monitoring
        // Record method execution times, call counts, and basic metrics
    }

    public void generatePerformanceReport() {
        // Generate basic performance analysis report
    }
}
```
**Deliverables:**
- ByteBuddy-based instrumentation engine
- CLI interface for instrumenting classes
- Basic performance metrics collection (timing, call counts)
- Simple text-based performance report

**Success Criteria:**
- [ ] Can instrument any Java class at runtime using ByteBuddy
- [ ] Records method execution times with <5% performance overhead
- [ ] Provides CLI interface for easy instrumentation
- [ ] Generates basic performance metrics and reports

## Week 2: Advanced Instrumentation & Memory Analysis

### Learning Materials
**Books:**
- *Java Performance* by Scott Oaks - Continue Chapter 2 (1 hour)

**Specifications:**
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 3: "Compiling for the Java Virtual Machine" (2 hours)
- [JVM Specification SE 21](https://docs.oracle.com/javase/specs/jvms/se21/html/) - Chapter 4: "The class File Format" (3 hours)

**Advanced ByteBuddy & Metrics:**
- [Micrometer Metrics Documentation](https://micrometer.io/docs) - Core concepts (1.5 hours)
- [ByteBuddy Advanced Features](https://bytebuddy.net/#/tutorial-advanced) - Interceptors and Annotations (1.5 hours)

**Online Resources:**
- [Oracle Bytecode Tutorial](https://docs.oracle.com/javase/specs/jvms/se21/html/jvms-6.html) (1 hour)
- [Performance Monitoring Best Practices](https://www.baeldung.com/micrometer) (1 hour)

### Hands-on Activities
1. **Memory Allocation Tracking** (3 hours)
   ```java
   // Instrument constructors to track object allocation
   new ByteBuddy()
       .redefine(targetClass)
       .constructor(ElementMatchers.any())
       .intercept(MethodDelegation.to(MemoryAllocationInterceptor.class))
       .make()
       .load(targetClass.getClassLoader());
   ```
   - Track object creation and memory usage patterns
   - Monitor large object allocations
   - Analyze allocation hotspots

2. **Hot Method Detection** (2 hours)
   - Implement statistical analysis of method call frequency
   - Build heat map of application performance bottlenecks
   - Create automated hotspot detection algorithms

### Projects
**Project 2: Memory & Performance Analytics Engine** (4 hours)
```java
// Goal: Advanced performance monitoring with memory allocation tracking
public class PerformanceAnalyticsEngine {
    // Features:
    // - Memory allocation tracking by class/method
    // - Hot method detection with statistical analysis
    // - Database query performance monitoring (JDBC)
    // - Real-time metrics dashboard with WebSocket updates

    public void trackMemoryAllocations(String className) {
        // Instrument constructors for memory tracking
    }

    public List<HotMethod> getHotMethods(int topN) {
        // Return top N methods by execution time/frequency
    }

    public void startRealTimeDashboard(int port) {
        // Launch web dashboard with live metrics
    }
}
```
**Deliverables:**
- Advanced instrumentation engine with memory tracking
- Hot method detection with statistical analysis
- Basic web dashboard for real-time monitoring
- JDBC query performance monitoring

**Success Criteria:**
- [ ] Tracks memory allocations and identifies allocation hotspots
- [ ] Detects hot methods with statistical significance
- [ ] Monitors database query performance automatically
- [ ] Provides real-time web dashboard with live metrics updates

## Week 3: Production Features & Spring Boot Integration

### Learning Materials
**Books:**
- Review *Java Performance* Chapters 1-2 (1 hour)

**Spring Boot & Production:**
- [Spring Boot Actuator Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html) (2 hours)
- [Spring Boot Metrics Integration](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html#actuator.metrics) (1.5 hours)

**Advanced Instrumentation:**
- [Java Agent Development](https://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html) (2 hours)
- [Production Monitoring Best Practices](https://www.baeldung.com/java-application-monitoring-tools) (1.5 hours)

**Online Resources:**
- [OpenJDK Wiki: HotSpot Glossary](https://wiki.openjdk.org/display/HotSpot/Glossary) (1 hour)
- [JVM Startup Process Deep Dive](https://shipilev.net/jvm/anatomy-quarks/) - Relevant articles (1 hour)

### Hands-on Activities
1. **Smart Sampling & Filtering** (3 hours)
   ```java
   // Implement adaptive sampling to reduce overhead
   public class AdaptiveSamplingStrategy {
       public boolean shouldSample(String methodName, long estimatedDuration) {
           // Reduce sampling for high-frequency methods
           // Maintain statistical significance
       }
   }
   ```
   - Build intelligent method filtering (skip getters/setters)
   - Implement adaptive sampling based on call frequency
   - Test overhead impact under different loads

2. **Spring Boot Auto-Configuration** (2 hours)
   - Create Spring Boot starter for automatic instrumentation
   - Implement configuration properties for production use
   - Add health checks and metrics endpoints

### Projects
**Project 3: Production-Ready Performance Instrumentation Tool** (4 hours)
```java
// Goal: Complete production-ready performance monitoring solution
@SpringBootApplication
@EnableConfigurationProperties(InstrumentationProperties.class)
public class PerformanceMonitoringStarter {
    // Features:
    // - Spring Boot auto-configuration and starter
    // - Intelligent sampling to minimize overhead (<1%)
    // - Production-ready filtering and configuration
    // - Integration with Spring Boot Actuator
    // - Docker deployment with monitoring dashboard

    @Bean
    @ConditionalOnProperty("performance.instrumentation.enabled")
    public PerformanceInstrumentationEngine instrumentationEngine() {
        return new PerformanceInstrumentationEngine();
    }
}
```
**Deliverables:**
- Complete Spring Boot starter with auto-configuration
- Production-ready sampling and filtering strategies
- Docker deployment with web dashboard
- Comprehensive documentation and usage examples
- Integration tests and performance benchmarks

**Success Criteria:**
- [ ] <1% performance overhead in production environments
- [ ] Spring Boot auto-configuration works out-of-the-box
- [ ] Intelligent filtering reduces noise and focuses on important metrics
- [ ] Docker deployment ready with monitoring dashboard
- [ ] Comprehensive documentation for production use

## Weekly Checkpoints

### Week 1 Checkpoint
- [ ] Can explain JVM memory areas and their purposes
- [ ] Successfully built ByteBuddy-based instrumentation engine
- [ ] Comfortable with basic performance metrics collection
- [ ] Understanding of method interception and bytecode manipulation

### Week 2 Checkpoint
- [ ] Can track memory allocations and identify hotspots
- [ ] Built advanced performance analytics with hot method detection
- [ ] Understands relationship between bytecode and performance
- [ ] Created real-time monitoring dashboard with live metrics

### Week 3 Checkpoint
- [ ] Built production-ready performance monitoring solution
- [ ] Implemented intelligent sampling and filtering strategies
- [ ] Comfortable with Spring Boot integration and auto-configuration
- [ ] Ready to deploy performance monitoring in production environments

## Tools Setup
Ensure you have these tools installed and configured:
- **OpenJDK 21** with source code
- **IntelliJ IDEA** with bytecode viewer plugin
- **Maven or Gradle** for project management
- **ByteBuddy** library dependency
- **Micrometer** for metrics collection
- **Spring Boot** framework
- **Docker** for containerized deployment

## Essential Dependencies
```xml
<!-- Core ByteBuddy for instrumentation -->
<dependency>
    <groupId>net.bytebuddy</groupId>
    <artifactId>byte-buddy</artifactId>
    <version>1.14.9</version>
</dependency>

<!-- Micrometer for metrics -->
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-core</artifactId>
    <version>1.12.0</version>
</dependency>

<!-- Spring Boot for production integration -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

## Troubleshooting Common Issues
1. **ByteBuddy transformation failures**: Check Java module system compatibility
2. **High instrumentation overhead**: Implement proper sampling strategies
3. **Memory leaks from instrumentation**: Ensure proper cleanup of interceptors
4. **Spring Boot integration issues**: Verify auto-configuration conditions

## Practical Usage Examples
```bash
# Basic instrumentation via CLI
java -jar performance-tool.jar --instrument-class=com.example.UserService

# Spring Boot application configuration
# application.yml
performance:
  instrumentation:
    enabled: true
    packages:
      - com.example.service
    sampling-rate: 0.05

# Docker deployment
docker run -p 8080:8080 performance-monitor:latest
```

## Next Week Preview
Week 4-5 will focus on memory management and garbage collection, building on the JVM structure knowledge from these weeks.