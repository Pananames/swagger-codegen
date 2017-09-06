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

Generate new template:
-----------------------------------
Move .swagger-codegen-ignore to library output DIR

```
sudo ./run-in-docker.sh generate -i template/config.yaml -l php -o /gen/out/Pananames -t template/php --invoker-package 'Pananames' --git-user-id 'pananames' --git-repo-id 'php-api' --artifact-version '2.0.0'
```

-----------------------------------
DOCS
-----------------------------------
https://github.com/swagger-api/swagger-codegen/wiki/Building-your-own-Templates

https://github.com/swagger-api/swagger-codegen/wiki/FAQ
