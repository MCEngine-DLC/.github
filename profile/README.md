# ExampleDLC for MCEngine Artificial Intelligence

This is an example DLC module for the `MCEngineArtificialIntelligence` plugin. It demonstrates how to implement and register a custom DLC using the provided `IMCEngineArtificialIntelligenceDLC` interface.

## 📦 Dependency Setup

To access GitHub Packages, you need to create a `.env` file in the root of your project and generate a personal access token with proper permissions.

```env
GIT_USER_NAME={your name}
GIT_USER_TOKEN={your token}
```

**Note:**
- Your token must have the `read:packages` permission enabled.
- Public GitHub packages can be accessed using a token, even if the user is not part of the organization or repository.

Add the `mcengine-artificialintelligence-api` to your project:

### ➤ Maven Repository
```xml
<repositories>
    <repository>
        <id>github</id>
        <url>https://maven.pkg.github.com/MCEngine/artificialintelligence</url>
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
  <artifactId>mcengine-artificialintelligence-api</artifactId>
  <version>{version}</version>
</dependency>
```

### ➤ Gradle Repository
```groovy
repositories {
    maven {
        url = uri('https://maven.pkg.github.com/MCEngine/artificialintelligence')
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
    implementation group: 'io.github.mcengine', name: 'mcengine-artificialintelligence-api', version: '{version}'
}
```

### ➤ Gradle (short form)
```groovy
implementation 'io.github.mcengine:mcengine-artificialintelligence-api:{version}'
```

---

## 🎮 Implementing a DLC

Your DLC class must implement the following interface:

```java
public interface IMCEngineArtificialIntelligenceDLC {
    void onLoad(Plugin plugin);
}
```

### ✅ Example Implementation

```java
package io.github.mcengine.dlc.example;

import io.github.mcengine.api.artificialintelligence.dlc.IMCEngineArtificialIntelligenceDLC;
import io.github.mcengine.api.artificialintelligence.dlc.MCEngineArtificialIntelligenceDLCLogger;
import org.bukkit.plugin.Plugin;

public class ExampleDLC implements IMCEngineArtificialIntelligenceDLC {

    private MCEngineArtificialIntelligenceDLCLogger logger;

    @Override
    public void onLoad(Plugin plugin) {
        logger = new MCEngineArtificialIntelligenceDLCLogger(plugin, "ExampleDLC");
        logger.info("ExampleDLC is loading...");
        
        // Add your DLC-specific logic here

        logger.info("ExampleDLC has loaded successfully.");
    }
}
```

---

## 📁 Packaging

Make sure your JAR file includes the `ExampleDLC` class and any required dependencies. Place the JAR in the `plugins/MCEngineArtificialIntelligence/dlcs/` folder.

---

## 🔄 Dynamic Loading

The core MCEngine plugin will detect and load this DLC automatically if it implements the interface `IMCEngineArtificialIntelligenceDLC`.

---
