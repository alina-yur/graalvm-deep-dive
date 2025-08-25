# GraalVM Deep Dive


**Bring the Action: Using GraalVM in Production (recording)**
<div align="center">
  <a href="https://www.youtube.com/watch?v=VVUngUrMjAo">
    <img src="https://img.youtube.com/vi/VVUngUrMjAo/sddefault.jpg">
  </a>
</div>

## Structure
* GraalVM overview 🐰
* Migrating an app to GraalVM 🤖
  * 👩‍💻 use Native Build Tools 🛠️
  * 👩‍💻 basic performance measurements with `time` 📈
* Using libraries 📚
  * A library might be designed to be Native-Image friendly out of the box;
  * A library might add config files to its source code;
  * Library configuration can be provided via GraalVM Reachability Metadata Repository;
  * 👩‍💻 You can programmatically generate configuration via framework annotations, such as `@ReflectiveAccess` ([Micronaut](https://guides.micronaut.io/latest/micronaut-graalvm-reflection-maven-java.html))
  * You can use Native Image's Tracing Agent (`java -agentlib:native-image-agent -jar ./target/demo.jar`)
```);
  * You can provide configuration manually via json.
* Performance optimizations 🚀
  * [Overview of compiler optimization levels](https://github.com/alina-yur/native-spring-boot?tab=readme-ov-file#optimization-levels-in-native-image)
  * 👩‍💻 PGO
    * ML-enabled PGO
    * You get [LCOV](https://www.graalvm.org/latest/reference-manual/native-image/optimizations-and-performance/PGO/LCOV/) info as a side product of PGO
  * G1 GC
  * `-march=native`
  * Memory management (`xmx`)
  * Demo: [spring-petclinic](https://github.com/spring-projects/spring-petclinic)
* Testing 👨‍🔬
* Deployment 📦
  * 👩‍💻 Packaging and linking options
    * JDK 
    * JDK | Distroless
    * JDK | JLink
    * Native | Dynamic |
      * `docker build -f Dockerfiles/Dockerfile.native -t native-spring-boot-native:latest .`
      * `docker run -p 8080:8080 native-spring-boot-native:latest .`
    * Native | Mostly static | Distroless
    * Native | Static | From scratch 
    * Native | Static | From scratch | Optimize for size
  * Scan the images for vulnerabilities & packages 🛡️
  * Buildpacks
  * GitHub actions
* Security 🛡️
  *  Security by design
  * 👩‍💻 Vulnerability Scanning
    * `grype`: `native-image-inspect --sbom ./target/demo-sbom | grype -v`
    * `native-image-inspect --sbom ./target/demo-sbom>output.json`
  * 👩‍💻 SBOM support: exposing in Spring Actuator
  * 👩‍💻 SBOM support in Micronaut
  * GitHub Action
  * Demo: [native-spring-boot-sbom](https://github.com/alina-yur/native-spring-boot-sbom)
* Monitoring 📈
  * 👩‍💻 Micrometer
    * (Tempo -> service graph)
  * 👩‍💻 `jvmstat` <!-- visualvm --jdkhome /Users/ayurenko/.sdkman/candidates/java/23-graal --> 
  * JFR, JMX, `jcmd`
  * `perf stat <process>`
* Tooling 🔮
  * 👩‍💻 Build reports
* In the lab 👩‍🔬
  * Some of our research project slogans
    * _"Why do it? Because we can"_
    * _"We do these things not because they are easy, but because we thought they were going to be easy"_
  * [Llama3.java]|(https://github.com/mukel/llama3.java)
  * [Native Image Layers](https://github.com/oracle/graal/issues/7626)
  * [Project Crema](https://github.com/orgs/oracle/projects/6?pane=issue&itemId=113766307&issue=oracle%7Cgraal%7C11327)
  * [`-H:Preserve=all`](https://github.com/oracle/graal/pull/10180)
  * Embedding Python (Pygal charts)
  * Wasm backend for Native Image (javac)
