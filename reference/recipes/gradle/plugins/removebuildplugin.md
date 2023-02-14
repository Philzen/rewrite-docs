# Remove plugin from `build.gradle(.kts)`

**org.openrewrite.gradle.plugins.RemoveBuildPlugin**
_Remove plugin from `build.gradle(.kts)`._

## Source

[Github](https://github.com/openrewrite/rewrite/tree/main/rewrite-gradle), [Issue Tracker](https://github.com/openrewrite/rewrite/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite/rewrite-gradle/7.36.0-SNAPSHOT/jar)

* groupId: org.openrewrite
* artifactId: rewrite-gradle
* version: 7.36.0-SNAPSHOT

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | pluginId | The plugin id to remove. |


## Usage

This recipe has required configuration parameters. Recipes with required configuration parameters cannot be activated directly. To activate this recipe you must create a new recipe which fills in the required parameters. In your rewrite.yml create a new recipe with a unique name. For example: `com.yourorg.RemoveBuildPluginExample`.
Here's how you can define and customize such a recipe within your rewrite.yml:

{% code title="rewrite.yml" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.RemoveBuildPluginExample
displayName: Remove plugin from `build.gradle(.kts)` example
recipeList:
  - org.openrewrite.gradle.plugins.RemoveBuildPlugin:
      pluginId: com.jfrog.bintray
```
{% endcode %}

Now that `com.yourorg.RemoveBuildPluginExample` has been defined activate it and take a dependency on org.openrewrite:rewrite-gradle:7.36.0-SNAPSHOT in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.34.0")
}

rewrite {
    activeRecipe("com.yourorg.RemoveBuildPluginExample")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite:rewrite-gradle:7.36.0-SNAPSHOT")
}
```
{% endcode %}
{% endtab %}

{% tab title="Maven" %}
{% code title="pom.xml" %}
```markup
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>4.39.0</version>
        <configuration>
          <activeRecipes>
            <recipe>com.yourorg.RemoveBuildPluginExample</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite</groupId>
            <artifactId>rewrite-gradle</artifactId>
            <version>7.36.0-SNAPSHOT</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-Drewrite.activeRecipes=com.yourorg.RemoveBuildPluginExample`

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://public.moderne.io/recipes/org.openrewrite.gradle.plugins.RemoveBuildPlugin)

The Moderne public SaaS instance enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.