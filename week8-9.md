# Week 8-9: Advanced Profiling & Native Memory

## Learning Objectives
By the end of these 2 weeks, you will:
- [ ] Master async-profiler for low-overhead production profiling
- [ ] Use Java Flight Recorder (JFR) for comprehensive application monitoring
- [ ] Track and optimize native memory usage outside the heap
- [ ] Profile real applications and identify performance bottlenecks
- [ ] Implement custom profiling solutions for specific use cases

## Time Allocation (30 hours total)
- **Reading/Study**: 12 hours (40%)
- **Hands-on Practice**: 10.5 hours (35%)
- **Projects**: 7.5 hours (25%)

## Week 8: async-profiler & Production Profiling

### Learning Materials
**Documentation:**
- [async-profiler GitHub](https://github.com/jvm-profiling-tools/async-profiler) - Complete README and wiki (2 hours)
- [async-profiler Profiling Guide](https://github.com/jvm-profiling-tools/async-profiler/blob/master/docs/ProfilingModes.md) (1.5 hours)

**Articles & Blogs:**
- [Profiling Java Applications in Production](https://www.baeldung.com/java-profilers) (1 hour)
- [Low-overhead Profiling with async-profiler](https://krzysztofslusarski.github.io/2022/12/12/async-profiler.html) (1 hour)
- [CPU Profiling Best Practices](https://netflixtechblog.com/java-in-flames-e763b3d32166) - Netflix Tech Blog (1 hour)

**Conference Talks:**
- [Profiling the Profilers](https://www.youtube.com/watch?v=plYESjZ9hUU) - Andrei Pangin at Devoxx (1 hour)
- [Advanced Profiling Techniques](https://www.youtube.com/watch?v=ugRrFdda_JQ) - JVM Language Summit (1.5 hours)

**Research Papers:**
- [Statistical Profiling in the Java HotSpot VM](https://www.usenix.org/legacy/events/jvm01/full_papers/click/click.pdf) (1 hour)

### Hands-on Activities
1. **async-profiler Mastery** (3.5 hours)
   ```bash
   # CPU profiling with flame graphs
   java -jar async-profiler.jar -e cpu -d 30 -f profile.html <pid>

   # Memory allocation profiling
   java -jar async-profiler.jar -e alloc -d 30 -f alloc.html <pid>

   # Lock contention profiling
   java -jar async-profiler.jar -e lock -d 30 -f locks.html <pid>

   # Wall-clock profiling (includes I/O wait)
   java -jar async-profiler.jar -e wall -d 30 -f wall.html <pid>

   # Advanced: Custom events and JFR integration
   java -jar async-profiler.jar -e cpu -o jfr -f profile.jfr <pid>
   ```

2. **Production Profiling Simulation** (2 hours)
   - Set up realistic load testing environment
   - Practice profiling under different load conditions
   - Compare profiling overhead across different tools

### Projects
**Project 1: Production Profiling Dashboard** (4 hours)
```java
// Goal: Build a web-based profiling dashboard for production monitoring
public class ProfilingDashboard {
    // Features:
    // - Integration with async-profiler
    // - Real-time flame graph generation
    // - Historical performance trending
    // - Automated hotspot detection
    // - Alert system for performance anomalies
}
```

**Deliverables:**
- Web dashboard with real-time profiling capabilities
- RESTful API for profiling control and data retrieval
- Automated flame graph generation and comparison
- Performance regression detection with alerting
- Docker container for easy deployment

**Success Criteria:**
- [ ] <1% overhead during profiling in production
- [ ] Generates actionable performance insights
- [ ] Integrates with common monitoring stacks (Prometheus/Grafana)
- [ ] Handles high-throughput applications (>10k RPS)

## Week 9: Java Flight Recorder & Native Memory Tracking

### Learning Materials
**Official Documentation:**
- [Java Flight Recorder Guide](https://docs.oracle.com/javacomponents/jmc-5-4/jfr-runtime-guide/about.htm) - Oracle JFR Documentation (2 hours)
- [Java Mission Control User Guide](https://docs.oracle.com/javacomponents/jmc-5-5/jmc-user-guide/intro.htm) (2 hours)

**Advanced Resources:**
- [Custom JFR Events](https://docs.oracle.com/en/java/javase/17/jfapi/creating-and-configuring-events.html) (1.5 hours)
- [Native Memory Tracking](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr007.html) - Oracle Documentation (1 hour)

**Articles:**
- [JFR in Production](https://bell-sw.com/announcements/2020/03/31/java-flight-recorder-in-production-tips-and-tricks/) (1 hour)
- [Understanding Native Memory Usage](https://www.baeldung.com/native-memory-tracking-in-jvm) (1 hour)
- [JFR Event Streaming](https://inside.java/2020/08/18/jfr-event-streaming/) (30 minutes)

**Video Resources:**
- [JFR and JMC Deep Dive](https://www.youtube.com/watch?v=7z_R2Aq-Fl8) - Oracle Code One (1 hour)
- [Advanced JFR Usage](https://www.youtube.com/watch?v=plYESjZ9hUU) - Production monitoring techniques (1 hour)

### Hands-on Activities
1. **JFR Comprehensive Profiling** (3 hours)
   ```bash
   # Continuous JFR recording for production
   java -XX:+FlightRecorder \
        -XX:StartFlightRecording=name=production,filename=app.jfr,maxsize=100m,maxage=1h \
        -XX:FlightRecorderOptions=settings=profile \
        YourApplication

   # Custom JFR settings file
   java -XX:+FlightRecorder \
        -XX:StartFlightRecording=settings=custom-profile.jfc,filename=custom.jfr \
        YourApplication

   # JFR event streaming (Java 14+)
   RecordingStream rs = new RecordingStream();
   rs.onEvent("jdk.CPULoad", System.out::println);
   rs.start();
   ```

2. **Native Memory Analysis** (2.5 hours)
   ```bash
   # Enable native memory tracking
   java -XX:NativeMemoryTracking=detail YourApplication

   # Monitor native memory usage
   jcmd <pid> VM.native_memory summary
   jcmd <pid> VM.native_memory detail
   jcmd <pid> VM.native_memory baseline
   jcmd <pid> VM.native_memory summary.diff

   # Analyze direct memory allocation
   jcmd <pid> VM.classloader_stats
   ```

### Projects
**Project 2: JFR Analysis Automation Suite** (3.5 hours)
```java
// Goal: Automated JFR analysis with custom event processing
public class JFRAnalysisSuite {
    // Features:
    // - Automated JFR file parsing and analysis
    // - Custom performance metrics extraction
    // - Trend analysis across multiple recordings
    // - Integration with APM systems
    // - Performance regression detection
}
```

**Deliverables:**
- JFR file parser with custom event extraction
- Performance metrics dashboard with historical trends
- Automated analysis reports with recommendations
- Integration APIs for APM tools (New Relic, AppDynamics)
- CLI tool for batch JFR analysis

**Success Criteria:**
- [ ] Processes large JFR files (>500MB) efficiently
- [ ] Extracts meaningful performance insights automatically
- [ ] Integrates with existing monitoring infrastructure
- [ ] Provides actionable optimization recommendations

## Advanced Profiling Techniques

### Custom JFR Events
```java
// Creating application-specific JFR events
@Name("myapp.BusinessTransaction")
@Label("Business Transaction")
@Description("Custom business logic profiling")
@Category("Application")
public class BusinessTransactionEvent extends Event {
    @Label("Transaction Type")
    String transactionType;

    @Label("Duration")
    @Timespan(Timespan.MILLISECONDS)
    long duration;

    @Label("Success")
    boolean success;
}

// Usage in application code
public void processTransaction(String type) {
    BusinessTransactionEvent event = new BusinessTransactionEvent();
    event.transactionType = type;
    event.begin();
    try {
        // Business logic here
        event.success = true;
    } catch (Exception e) {
        event.success = false;
        throw e;
    } finally {
        event.end();
        event.commit();
    }
}
```

### Native Memory Deep Dive
```java
// Monitoring direct memory allocation
public class DirectMemoryMonitor {
    private static final MemoryMXBean memoryBean = ManagementFactory.getMemoryMXBean();

    public void monitorDirectMemory() {
        // Track ByteBuffer allocations
        long directMemory = getDirectMemoryUsage();

        // Monitor memory-mapped files
        long mappedMemory = getMappedMemoryUsage();

        // Track JNI allocations
        analyzeNativeMemoryTracking();
    }
}
```

### Lock Profiling Strategies
```bash
# async-profiler lock profiling
java -jar async-profiler.jar -e lock -d 60 -f locks.svg <pid>

# JFR lock analysis
java -XX:+FlightRecorder \
     -XX:StartFlightRecording=filename=locks.jfr,settings=profile \
     -XX:FlightRecorderOptions=settings=locks \
     YourApplication
```

## Performance Analysis Workflows

### Systematic Profiling Approach
1. **Baseline Establishment**
   - Record normal operation metrics
   - Establish performance SLAs
   - Document expected resource usage

2. **Hotspot Identification**
   - CPU profiling for computational bottlenecks
   - Memory profiling for allocation patterns
   - Lock profiling for contention points

3. **Root Cause Analysis**
   - Drill down into specific methods
   - Analyze call trees and flame graphs
   - Correlate with application logs

4. **Optimization Validation**
   - Before/after performance comparison
   - Regression testing
   - Production monitoring

### Profiling Data Correlation
```java
// Correlating JFR events with application metrics
public class ProfileDataCorrelator {
    public void analyzePerformanceIssue(Path jfrFile, LocalDateTime issueTime) {
        try (RecordingFile recording = new RecordingFile(jfrFile)) {
            // Find events around the issue time
            recording.readAllEvents().stream()
                .filter(event -> isAroundTime(event, issueTime))
                .forEach(this::analyzeEvent);
        }
    }
}
```

## Weekly Checkpoints

### Week 8 Checkpoint
- [ ] Can use async-profiler effectively for production profiling
- [ ] Understands flame graph analysis and interpretation
- [ ] Built working profiling dashboard for production use
- [ ] Can identify performance bottlenecks in real applications

### Week 9 Checkpoint
- [ ] Masters JFR for comprehensive application monitoring
- [ ] Can track and optimize native memory usage
- [ ] Created automated JFR analysis tools
- [ ] Understands correlation between different profiling data sources

## Tool Setup & Configuration

### async-profiler Installation
```bash
# Download latest release
wget https://github.com/jvm-profiling-tools/async-profiler/releases/download/v2.9/async-profiler-2.9-linux-x64.tar.gz
tar xzf async-profiler-2.9-linux-x64.tar.gz

# Ensure proper permissions for profiling
echo 1 | sudo tee /proc/sys/kernel/perf_event_paranoid
echo 0 | sudo tee /proc/sys/kernel/kptr_restrict
```

### JFR Configuration Templates
```xml
<!-- custom-profile.jfc - Optimized for production use -->
<configuration version="2.0" label="Custom Production Profile">
  <event name="jdk.CPULoad">
    <setting name="enabled">true</setting>
    <setting name="period">1000 ms</setting>
  </event>
  <event name="jdk.ExecutionSample">
    <setting name="enabled">true</setting>
    <setting name="period">10 ms</setting>
  </event>
  <!-- Add more events as needed -->
</configuration>
```

### Native Memory Tracking Setup
```bash
# Production-friendly NMT settings
-XX:NativeMemoryTracking=summary  # Lower overhead than 'detail'
-XX:+PrintNMTStatistics          # Print NMT data on JVM exit
```

## Production Profiling Best Practices

### Overhead Considerations
- **async-profiler**: <1% CPU overhead in sampling mode
- **JFR**: <2% overhead with default settings
- **NMT**: <1% memory overhead for tracking

### Profiling Scheduling
- **Continuous profiling**: 24/7 with low overhead settings
- **Deep profiling**: Scheduled during low-traffic periods
- **Incident response**: On-demand profiling with higher overhead acceptable

### Data Management
- **Retention**: Keep profiling data for 30-90 days
- **Compression**: Use automated compression for storage efficiency
- **Access control**: Secure profiling data access in production

## Troubleshooting Common Issues

### Profiling Problems
1. **High overhead**: Reduce sampling frequency or event selection
2. **Missing symbols**: Ensure debug symbols available
3. **Incomplete profiles**: Check permissions and system limits

### Analysis Challenges
1. **Noisy data**: Use longer profiling periods for statistical significance
2. **False hotspots**: Correlate with actual performance metrics
3. **Version differences**: Account for JVM version changes in analysis

## Next Week Preview
Week 10-12 will focus on virtual threads and structured concurrency, building on the profiling skills developed in these weeks to analyze modern concurrency patterns.