### maven plugin
    <plugin>
     <groupId>org.owasp</groupId>
     <artifactId>dependency-check-maven</artifactId>
     <version>10.0.4</version>
     <configuration>
        <format>ALL</format>
        <failBuildOnCVSS>8</failBuildOnCVSS>
     </configuration>
    </plugin>

### github
    https://github.com/jeremylong/DependencyCheck