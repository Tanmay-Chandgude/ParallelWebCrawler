# Parallel Web Crawler

A high-performance, multi-threaded web crawler built in Java using the Fork/Join Framework. This project was developed as part of the Udacity Advanced Java Programming Techniques course and demonstrates concurrent programming, dependency injection, JSON processing, functional programming, and dynamic proxy-based profiling.

## Features

- Multi-threaded web crawling using `ForkJoinPool`
- Recursive parallel URL traversal
- Thread-safe word frequency counting
- Configurable crawl depth, timeout, and parallelism
- JSON-based configuration and output
- Dynamic proxy-based performance profiler
- Functional programming with Java Streams
- Maven-based project structure
- Dependency Injection using Google Guice

---

## Technologies Used

- Java 25
- Maven
- Google Guice
- Jackson Databind
- ForkJoinPool
- Java Streams API
- Dynamic Proxies (Reflection)
- JUnit

---

## Project Structure

```text
src/
├── main/
│   ├── java/
│   │   └── com/udacity/webcrawler/
│   └── resources/
├── test/
│   └── java/
pom.xml
```

---

## Configuration

Crawler settings are defined using a JSON configuration file.

Example:

```json
{
  "startPages": ["https://openlibrary.org/"],
  "ignoredUrls": [
    "https://openlibrary.org/about.*",
    "https://openlibrary.org/people.*"
  ],
  "ignoredWords": ["^.{1,3}$"],
  "parallelism": 4,
  "maxDepth": 10,
  "timeoutSeconds": 1,
  "popularWordCount": 5,
  "profileOutputPath": "profileData.txt"
}
```

### Configuration Options

| Option | Description |
|----------|-------------|
| startPages | URLs where crawling begins |
| ignoredUrls | Regex patterns of URLs to skip |
| ignoredWords | Regex patterns of words to ignore |
| parallelism | Number of worker threads |
| maxDepth | Maximum crawl depth |
| timeoutSeconds | Maximum crawl duration |
| popularWordCount | Number of top words returned |
| profileOutputPath | Path for profiler output |

---

## Build Project

```bash
mvn clean package
```

---

## Run the Application

```bash
java -classpath target/udacity-webcrawler-1.0.jar \
com.udacity.webcrawler.main.WebCrawlerMain \
src/main/java/com/udacity/webcrawler/main/config/sample_config.json
```

Windows PowerShell:

```powershell
java -classpath target/udacity-webcrawler-1.0.jar com.udacity.webcrawler.main.WebCrawlerMain src/main/java/com/udacity/webcrawler/main/config/sample_config.json
```

---

## Sample Output

### Crawl Result

```json
{
  "wordCounts": {
    "library": 36,
    "borrow": 29,
    "books": 29,
    "book": 18,
    "search": 16
  },
  "urlsVisited": 5
}
```

### Profiling Output

```text
Run at Sun, 21 Jun 2026 07:13:48 GMT
com.udacity.webcrawler.ParallelWebCrawler#crawl took 0m 2s 390ms
com.udacity.webcrawler.parser.PageParserImpl#parse took 0m 2s 369ms
```

---

## Parallel Crawling Architecture

1. Start crawling from configured URLs.
2. Create a `CrawlTask` for each URL.
3. Submit tasks to a `ForkJoinPool`.
4. Parse pages concurrently.
5. Aggregate word counts using thread-safe collections.
6. Track visited URLs to prevent duplicate processing.
7. Return the most frequent words.

---

## Performance Profiling

The application includes a custom profiler built using Java Dynamic Proxies.

### Features

- Profiles only methods annotated with `@Profiled`
- Records execution time
- Aggregates multiple invocations
- Handles exceptions correctly
- Thread-safe implementation

---

## Testing

Run all tests:

```bash
mvn test
```

Run specific tests:

```bash
mvn test -Dtest=ConfigurationLoaderTest
mvn test -Dtest=CrawlResultWriterTest
mvn test -Dtest=ParallelWebCrawlerTest
mvn test -Dtest=WordCountsTest
mvn test -Dtest=ProfilerImplTest
```

---

## Key Concepts Demonstrated

- Concurrent Programming
- Fork/Join Framework
- Dependency Injection
- Dynamic Proxies
- Reflection API
- Functional Programming
- JSON Serialization/Deserialization
- Thread Safety
- Recursive Algorithms
- Maven Build Automation

---

## Learning Outcomes

Through this project, I gained hands-on experience with:

- Designing scalable concurrent applications
- Implementing thread-safe data structures
- Using Google Guice for dependency injection
- Building dynamic proxy-based profilers
- Writing functional-style Java code using Streams
- Managing Maven projects and automated testing

---

## Author

**Tanmay Chandgude**

- GitHub: https://github.com/Tanmay-Chandgude

---

## License

This project was developed for educational purposes as part of the Udacity Advanced Java Programming Techniques course.
