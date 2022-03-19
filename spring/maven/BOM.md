# Bill of Materials.

The combination of dependency that works togeather . This  is a way to define a collection of jars togeather to work in a project .

## what is a Pom
Maven POM is an XML file that contains information and configurations (about the project) that are used by Maven to import dependencies and to build the project.

BOM stands for Bill Of Materials. **A BOM is a special kind of POM that is used to control the versions of a project’s dependencies and provide a central place to define and update those versions.**

BOM provides the flexibility to add a dependency to our module without worrying about the version that we should depend on.



### *When we have a set of projects that inherit a common parent, we can put all dependency information in a shared POM file called BOM.*



```xml
<project >
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Baeldung-BOM</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>BaelDung-BOM</name>
    <description>parent pom</description>
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>test</groupId>
                <artifactId>a</artifactId>
                <version>1.2</version>
            </dependency>
            <dependency>
                <groupId>test</groupId>
                <artifactId>b</artifactId>
                <version>1.0</version>
                <scope>compile</scope>
            </dependency>
            <dependency>
                <groupId>test</groupId>
                <artifactId>c</artifactId>
                <version>1.0</version>
                <scope>compile</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```


## Using the BOM
 ### Inherit the project
```xml
<project >
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Test</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Test</name>
    <parent>
        <groupId>baeldung</groupId>
        <artifactId>Baeldung-BOM</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    </parent>
</project>
```

import the bom (big project)
```xml
<project ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Test</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Test</name>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>baeldung</groupId>
                <artifactId>Baeldung-BOM</artifactId>
                <version>0.0.1-SNAPSHOT</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```

## Override the BOM
The order of precedence of the artifact's version is:

1.  The version of the artifact's direct declaration in our project pom
2.  The version of the artifact in the parent project
3.  The version in the imported pom, taking into consideration the order of importing files
4.  dependency mediation

-   We can overwrite the artifact's version by explicitly defining the artifact in our project's pom with the desired version
-   If the same artifact is defined with different versions in 2 imported BOMs, then the version in the BOM file that was declared first will win