# Change `java.lang.reflect.Modifier` and ` java.lang.invoke.ConstantBootstraps` method calls to static

**org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors**

_The `java.lang.reflect.Modifier()` and `java.lang.invoke.ConstantBootstraps()` constructors have been removed in Java SE 15 because both classes only contain static methods. This recipe converts the usage of all methods in the two classes to be  static. For more information on these changes, see https://docs.oracle.com/en/java/javase/15/migrate/index.html#GUID-233853B8-0782-429E-BEF7-7532EE610E63_

## Recipe source

[GitHub](https://github.com/openrewrite/rewrite-migrate-java/blob/main/src/main/resources/META-INF/rewrite/java-version-17.yml), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://central.sonatype.com/artifact/org.openrewrite.recipe/rewrite-migrate-java/2.17.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 2.17.0

{% hint style="info" %}
This recipe is composed of more than one recipe. If you want to customize the set of recipes this is composed of, you can find and copy the GitHub source for the recipe from the link above.
{% endhint %}

## Usage

This recipe has no required configuration options. It can be activated by adding a dependency on `org.openrewrite.recipe:rewrite-migrate-java:2.17.0` in your build file or by running a shell command (in which case no build changes are needed): 
{% tabs %}
{% tab title="Gradle" %}
1. Add the following to your `build.gradle` file:
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("6.16.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:2.17.0")
}
```
{% endcode %}
2. Run `gradle rewriteRun` to run the recipe.
{% endtab %}

{% tab title="Gradle init script" %}
1. Create a file named `init.gradle` in the root of your project.
{% code title="init.gradle" %}
```groovy
initscript {
    repositories {
        maven { url "https://plugins.gradle.org/m2" }
    }
    dependencies { classpath("org.openrewrite:plugin:6.16.0") }
}
rootProject {
    plugins.apply(org.openrewrite.gradle.RewritePlugin)
    dependencies {
        rewrite("org.openrewrite.recipe:rewrite-migrate-java:2.17.0")
    }
    rewrite {
        activeRecipe("org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors")
    }
    afterEvaluate {
        if (repositories.isEmpty()) {
            repositories {
                mavenCentral()
            }
        }
    }
}
```
{% endcode %}
2. Run `gradle --init-script init.gradle rewriteRun` to run the recipe.
{% endtab %}
{% tab title="Maven POM" %}
1. Add the following to your `pom.xml` file:
{% code title="pom.xml" %}
```xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>5.33.0</version>
        <configuration>
          
          <activeRecipes>
            <recipe>org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
            <version>2.17.0</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
2. Run `mvn rewrite:run` to run the recipe.
{% endtab %}

{% tab title="Maven Command Line" %}

You will need to have [Maven](https://maven.apache.org/download.cgi) installed on your machine before you can run the following command.

{% code title="shell" overflow="wrap" %}
```shell
mvn -U org.openrewrite.maven:rewrite-maven-plugin:run -Drewrite.recipeArtifactCoordinates=org.openrewrite.recipe:rewrite-migrate-java:RELEASE -Drewrite.activeRecipes=org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors 
```
{% endcode %}
{% endtab %}
{% tab title="Moderne CLI" %}
You will need to have configured the [Moderne CLI](https://docs.moderne.io/moderne-cli/cli-intro) on your machine before you can run the following command.

{% code title="shell" %}
```shell
mod run . --recipe RemovedModifierAndConstantBootstrapsConstructors
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Change method target to static](../../java/changemethodtargettostatic.md)
  * methodPattern: `java.lang.reflect.Modifier *(..)`
  * fullyQualifiedTargetTypeName: `java.lang.reflect.Modifier`
* [Change method target to static](../../java/changemethodtargettostatic.md)
  * methodPattern: `java.lang.invoke.ConstantBootstraps *(..)`
  * fullyQualifiedTargetTypeName: `java.lang.invoke.ConstantBootstraps`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors
displayName: Change `java.lang.reflect.Modifier` and ` java.lang.invoke.ConstantBootstraps` method calls to static
description: The `java.lang.reflect.Modifier()` and `java.lang.invoke.ConstantBootstraps()` constructors have been removed in Java SE 15 because both classes only contain static methods. This recipe converts the usage of all methods in the two classes to be  static. For more information on these changes, see https://docs.oracle.com/en/java/javase/15/migrate/index.html#GUID-233853B8-0782-429E-BEF7-7532EE610E63

recipeList:
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: java.lang.reflect.Modifier *(..)
      fullyQualifiedTargetTypeName: java.lang.reflect.Modifier
  - org.openrewrite.java.ChangeMethodTargetToStatic:
      methodPattern: java.lang.invoke.ConstantBootstraps *(..)
      fullyQualifiedTargetTypeName: java.lang.invoke.ConstantBootstraps

```
{% endtab %}
{% endtabs %}

## See how this recipe works across multiple open-source repositories

[![Moderne Link Image](/.gitbook/assets/ModerneRecipeButton.png)](https://app.moderne.io/recipes/org.openrewrite.java.migrate.RemovedModifierAndConstantBootstrapsConstructors)

The community edition of the Moderne platform enables you to easily run recipes across thousands of open-source repositories.

Please [contact Moderne](https://moderne.io/product) for more information about safely running the recipes on your own codebase in a private SaaS.