# Description

This fork of [xerial/sqlite-jdbc](https://github.com/xerial/sqlite-jdbc) comes with the `decimal.c` extension
precompiled into the binary.

# Changes Compared to Source

1. Added `src/main/ext/decimal.c`
1. Added `src/main/ext/decimal_init.c`
1. Added `-DSQLITE_EXTRA_INIT=core_init` to build args in `Makefile` to enable the `decimal.c` extension by default
1. Removed sonatype parent
1. Changed groupId to `io.onecloud` for publishing to GitHub Packages
1. Added `<dependencyManagement />` block in `pom.xml` with GitHub Packages destination

# Updating

1. Fetch the latest changes from [xerial/sqlite-jdbc](https://github.com/xerial/sqlite-jdbc)
1. Fetch the latest version of `decimal.c` and copy into `src/main/ext`
1. If `decimal.c` contains the below block, delete it

```c
#ifdef _WIN32
__declspec(dllexport)
#endif
```

# Build Instructions

1. `make package` will build for all environments using docker containers
1. See the `Makefile` for more options

# Deploying to maven

1. In `~/.m2/settings.xml`

```xml

<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
    <activeProfiles>
        <activeProfile>github</activeProfile>
    </activeProfiles>

    <profiles>
        <profile>
            <id>github</id>
            <repositories>
                <repository>
                    <id>central</id>
                    <url>https://repo1.maven.org/maven2</url>
                </repository>
                <repository>
                    <id>github</id>
                    <url>https://maven.pkg.github.com/OneCloudInc/*</url>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
            </repositories>
        </profile>
    </profiles>

    <servers>
        <server>
            <id>github</id>
            <username>USERNAME</username>
            <password>GITHUB_TOKEN</password>
        </server>
    </servers>
</settings>
```

2. Then run `mvn deploy` 
