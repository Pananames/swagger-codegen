Generate library:
-----------------------------------

В корне swagger выполнить:

```
sudo ./run-in-docker.sh generate -i SDK/config.yaml -l php -o SDK/lib/Pananames -t SDK/template/ --invoker-package 'Pananames' --git-user-id 'pananames' --git-repo-id 'php-api' --artifact-version '2.0.0'
```
- i - путь к config-файлу yaml
- l - язык, с помощью которого генерировать библиотеку
- o - путь к директории, где будет сохранена сгенерированная библиотека
- t - путь к шаблону
- --invoker-package - имя пакета, используется для namespace

- --git-user-id - для composer.json
- --git-repo-id - для composer.json
- --artifact-version - для composer.json

-----------------------
Development in Docker
-----------------------

The transforming logic lives here:
```
modules/swagger-codegen/src/main/java/io/swagger/codegen/languages/PhpClientCodegen.java
```

We changed:
-----------------------------------
```
protected String packagePath = "";

supportingFiles.add(new SupportingFile("ApiClient.mustache", toPackagePath(invokerPackage, srcBasePath + "/" + apiDirName), "ApiClient.php"));

supportingFiles.add(new SupportingFile("ObjectSerializer.mustache", toPackagePath(invokerPackage, srcBasePath + "/" + apiDirName), "ObjectSerializer.php"));

```

Build package after changing the transforming logic:
-----------------------------------
```
sudo ./run-in-docker.sh mvn package
```

Generate new lib from template:
-----------------------------------
Move .swagger-codegen-ignore to library output DIR

```
sudo ./run-in-docker.sh generate -i config.yaml -l php -o output-dir -t path/to/template --invoker-package 'Package' --git-user-id 'git-user' --git-repo-id 'git-repo' --artifact-version 'lib-version'
```

-----------------------------------
DOCS
-----------------------------------
https://github.com/swagger-api/swagger-codegen/wiki/Building-your-own-Templates

https://github.com/swagger-api/swagger-codegen/wiki/FAQ
