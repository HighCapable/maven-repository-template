# maven-repository-template

[![GitHub license](https://img.shields.io/github/license/HighCapable/maven-repository-template?color=blue)](https://github.com/HighCapable/maven-repository-template/blob/main/LICENSE)

This is a simple Maven repository by using GitHub to manage dependencies.

You can fork this repository as a template to create your own personal Maven repository, provided it maintains and follows the `Apache-2.0` license.

这是一个使用 GitHub 管理依赖的简单 Maven 存储库。

你可以复刻此存储库作为模版创建自己的私人 Maven 存储库，但必须保持并遵循 `Apache-2.0` 许可协议。

## Usage

The directory `repository` is the repository, which contains two parts: `releases` (release version) and `snapshots` (snapshots), where all Maven project artifacts are stored.

Reference this repository using the link below.

> Releases

```
https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/releases
```

> SnapShots

```
https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/snapshots
```

### Usage in Gradle Projects

You can use this repository in any Gradle project.

#### Configure Repository

```kotlin
repositories {
    maven {
        name = "personal-maven-repository-releases"
        setUrl("https://raw.githubusercontent.com/[organization name or user name]/[repository name]/[branch name]/repository/releases")
    }
    maven {
        name = "personal-maven-repository-snapshots"
        setUrl("https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/snapshots")
    }
}
```

You can also use [SweetDependency](https://github/HighCapable/SweetDependency) to uniformly manage and set up repositories.

```yaml
repositories:
  personal-maven-repository-releases:
    url: https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/releases
  personal-maven-repository-snapshots:
    url: https://raw.githubusercontent.com/[organization name or username]/[repository name]/[branch name]/repository/snapshots
```

#### Publish Artifacts to Repository

It is recommended to use vanniktech's [gradle-maven-publish-plugin](https://vanniktech.github.io/gradle-maven-publish-plugin) to publish Maven artifacts.

Below is a reference for how to configure a repository to publish to.

You can publish the repository directly to the `.gradle/personal-maven-repository` directory under your local user directory, and then set `personal-maven-repository` as a git repository.

Connect the `personal-maven-repository` directory to GitHub.

After each release of artifacts, perform a `git commit` and `git push` to synchronize the current repository.

```kotlin
publishing {
    repositories {
        val repositoryDir = gradle.gradleUserHomeDir
            .resolve("personal-maven-repository")
            .resolve("repository")
        maven {
            name = "PersonalMavenReleases"
            url = repositoryDir.resolve("releases").toURI()
        }
        maven {
            name = "PersonalMavenSnapShots"
            url = repositoryDir.resolve("snapshots").toURI()
        }
    }
}
```

## 使用方法

目录 `repository` 即为存储库，其中包含了 `releases` (发行版) 和 `snapshots` (快照) 两部分，这里存放了所有 Maven 项目的工件。

使用以下链接引用此存储库。

> Releases

```
https://raw.githubusercontent.com/[组织名或用户名]/[存储库名]/[分支名]/repository/releases
```

> SnapShots

```
https://raw.githubusercontent.com/[组织名或用户名]/[存储库名]/[分支名]/repository/snapshots
```

针对中国大陆地区无法访问 `raw.githubusercontent.com` 可以使用加速服务，例如 [GitMirror](https://gitmirror.com/)。

### 在 Gradle 项目中使用

你可以在任意 Gradle 项目中使用此存储库。

#### 配置存储库

```kotlin
repositories {
    maven {
        name = "personal-maven-repository-releases"
        setUrl("https://raw.githubusercontent.com/[组织名或用户名]/[存储库名]/[分支名]/repository/releases")
    }
    maven {
        name = "personal-maven-repository-snapshots"
        setUrl("https://raw.githubusercontent.com/[组织名或用户名]/[存储库名]/[分支名]/repository/snapshots")
    }
}
```

你还可以使用 [SweetDependency](https://github/HighCapable/SweetDependency) 统一管理并设置存储库。

```yaml
repositories:
  personal-maven-repository-releases:
    url: https://raw.githubusercontent.com/[组织名或用户名]/[存储库名]/[分支名]/repository/releases
  personal-maven-repository-snapshots:
    url: https://raw.githubusercontent.com/[组织名或用户名]/[存储库名]/[分支名]/repository/snapshots
```

#### 发布工件到存储库

推荐使用 vanniktech 的 [gradle-maven-publish-plugin](https://vanniktech.github.io/gradle-maven-publish-plugin) 来发布 Maven 工件。

下面是一个配置发布到的存储库方式的参考。

你可以直接将存储库发布到本机用户目录下的 `.gradle/personal-maven-repository` 目录中，然后将 `personal-maven-repository` 设置为 git 存储库。

将 `personal-maven-repository` 目录连接到 GitHub。

每次发布工件后，进行一次 `git commit` 和 `git push` 即可同步当前存储库。

```kotlin
publishing {
    repositories {
        val repositoryDir = gradle.gradleUserHomeDir
            .resolve("personal-maven-repository")
            .resolve("repository")
        maven {
            name = "PersonalMavenReleases"
            url = repositoryDir.resolve("releases").toURI()
        }
        maven {
            name = "PersonalMavenSnapShots"
            url = repositoryDir.resolve("snapshots").toURI()
        }
    }
}
```

## License

- [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

```
Apache License Version 2.0

Copyright (C) 2019-2023 HighCapable

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

Copyright © 2019-2023 HighCapable
