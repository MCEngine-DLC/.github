# ExampleDLC for MCEngine Projects

This is an example DLC module for the `MCEngine{project name}` plugin. It demonstrates how to implement and register a custom DLC using the provided `IMCEngine{project name}DLC` interface.

## 📦 Dependency Setup

To access GitHub Packages, you need to create two environments for authentication in your GitHub project and generate a personal access token with the appropriate permissions.

```env
GIT_USER_NAME={your name}
GIT_USER_TOKEN={your token}
```

**Note:**
- Your token must have the `read:packages` permission enabled.
- Public GitHub packages can be accessed using a token, even if the user is not part of the organization or repository.

Add the `mcengine-{project name}-api` to your project:

### ➤ Maven Repository
```xml
<repositories>
    <repository>
        <id>github</id>
        <url>https://maven.pkg.github.com/MCEngine/{project name}</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
</repositories>

<servers>
    <server>
        <id>github</id>
        <username>${env.GIT_USER_NAME}</username>
        <password>${env.GIT_USER_TOKEN}</password>
    </server>
</servers>
```

### ➤ Maven
```xml
<dependency>
  <groupId>io.github.mcengine</groupId>
  <artifactId>mcengine-{project name}-api</artifactId>
  <version>{version}</version>
</dependency>
```

### ➤ Gradle Repository
```groovy
repositories {
    maven {
        url = uri('https://maven.pkg.github.com/MCEngine/{project name}')
        credentials {
            username = System.getenv('GIT_USER_NAME') ?: 'null'
            password = System.getenv('GIT_USER_TOKEN') ?: 'null'
        }
    }
}
```

### ➤ Gradle (long form)
```groovy
dependencies {
    implementation group: 'io.github.mcengine', name: 'mcengine-{project name}-api', version: '{version}'
}
```

### ➤ Gradle (short form)
```groovy
implementation 'io.github.mcengine:mcengine-{project name}-api:{version}'
```

---

## 🎮 Implementing a DLC

Your DLC class must implement the following interface:

```java
public interface IMCEngine{project name}DLC {
    void onLoad(Plugin plugin);
}
```

### ✅ Example Implementation

```java
package io.github.mcengine.dlc.example;

import io.github.mcengine.api.{project name}.dlc.IMCEngine{project name}DLC;
import io.github.mcengine.api.{project name}.dlc.MCEngine{project name}DLCLogger;
import org.bukkit.plugin.Plugin;

public class ExampleDLC implements IMCEngine{project name}DLC {

    private MCEngine{project name}DLCLogger logger;

    @Override
    public void onLoad(Plugin plugin) {
        logger = new MCEngine{project name}DLCLogger(plugin, "ExampleDLC");
        logger.info("ExampleDLC is loading...");
        
        // Add your DLC-specific logic here

        logger.info("ExampleDLC has loaded successfully.");
    }
}
```

---

## 📁 Packaging

Make sure your JAR file includes the `ExampleDLC` class and any required dependencies. Place the JAR in the `plugins/MCEngine{project name}/dlcs/` folder.

---

## 🔄 Dynamic Loading

The core MCEngine plugin will detect and load this DLC automatically if it implements the interface `IMCEngine{project name}DLC`.

---

<div align="center">

<h3><b>📦 Available Project</b></h3>

<a href="https://github.com/MCEngine-DLC/example"><code>Example</code></a>

<h3><b>📁 Projects</b></h3>

<table>
  <tr>
    <td><a href="https://github.com/MCEngine/artificialintelligence"><code>artificialintelligence</code></a></td>
  </tr>
</table>

</div>

---
