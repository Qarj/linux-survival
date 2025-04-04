# Java

## classpath errors with VSCode after adding a new subproject

CTRL + SHIFT + P --> Java: Clean Java Language Server Workspace

## Install Java 8 SDK

```sh
sudo apt install openjdk-8-jdk openjdk-8-jre
java -version
.
openjdk version "1.8.0_252"
OpenJDK Runtime Environment (build 1.8.0_252-8u252-b09-1ubuntu1-b09)
OpenJDK 64-Bit Server VM (build 25.252-b09, mixed mode)
```

## Set JAVA_HOME

```
ls /usr/lib/jvm/java-8-openjdk-amd64/
.
ASSEMBLY_EXCEPTION bin docs include jre lib man src.zip THIRD_PARTY_README
```

```sh
gedit /home/$USER/.bashrc
.
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
.
source /home/$USER/.bashrc
.
echo $JAVA_HOME
.
/usr/lib/jvm/java-8-openjdk-amd64
```

## .vscode/settings.json for Java with code formatting on save

```json
{
    "java.jdt.ls.java.home": "/usr/lib/jvm/java-11-amazon-corretto",
    "java.configuration.updateBuildConfiguration": "interactive",
    "editor.formatOnSave": true,
    "[java]": {
        "editor.defaultFormatter": "redhat.java"
    },
    "java.format.settings.url": "/home/user/project1/formatter.xml",
    "java.format.settings.profile": "RecommendedJavaStyle"
}
```

## Java Code Formatter - formatter.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<profiles version="1.0">
    <profile>
        <id>RecommendedJavaStyle</id>
        <name>Recommended Java Style</name>
        <settings>
            <!-- Indentation -->
            <setting id="org.eclipse.jdt.core.formatter.tabulation.char" value="space"/>
            <setting id="org.eclipse.jdt.core.formatter.tabulation.size" value="4"/>
            <setting id="org.eclipse.jdt.core.formatter.indentation.size" value="4"/>

            <!-- Braces -->
            <setting id="org.eclipse.jdt.core.formatter.brace_position_for_type_declaration" value="next_line"/>
            <setting id="org.eclipse.jdt.core.formatter.brace_position_for_method_declaration" value="next_line"/>
            <setting id="org.eclipse.jdt.core.formatter.brace_position_for_block" value="end_of_line"/>
            <setting id="org.eclipse.jdt.core.formatter.brace_position_for_switch" value="next_line"/>

            <!-- Line Wrapping -->
            <setting id="org.eclipse.jdt.core.formatter.line_split" value="120"/>
            <setting id="org.eclipse.jdt.core.formatter.wrap_before_binary_operator" value="true"/>
            <setting id="org.eclipse.jdt.core.formatter.wrap_before_assignment_operator" value="true"/>

            <!-- Blank Lines -->
            <setting id="org.eclipse.jdt.core.formatter.blank_lines_before_package" value="1"/>
            <setting id="org.eclipse.jdt.core.formatter.blank_lines_after_package" value="1"/>
            <setting id="org.eclipse.jdt.core.formatter.blank_lines_before_imports" value="1"/>
            <setting id="org.eclipse.jdt.core.formatter.blank_lines_after_imports" value="1"/>
            <setting id="org.eclipse.jdt.core.formatter.blank_lines_before_class_body" value="1"/>
            <setting id="org.eclipse.jdt.core.formatter.blank_lines_after_class_body" value="1"/>

            <!-- Comments -->
            <setting id="org.eclipse.jdt.core.formatter.comment.format_line_comment" value="true"/>
            <setting id="org.eclipse.jdt.core.formatter.comment.format_block_comment" value="true"/>
            <setting id="org.eclipse.jdt.core.formatter.comment.format_javadoc_comment" value="true"/>
            <setting id="org.eclipse.jdt.core.formatter.comment.insert_new_line_before_root_tags" value="true"/>
            <setting id="org.eclipse.jdt.core.formatter.comment.new_lines_at_javadoc_boundaries" value="true"/>
        </settings>
    </profile>
</profiles>
```
