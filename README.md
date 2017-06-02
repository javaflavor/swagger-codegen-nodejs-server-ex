# Implementing Additional Language Extension for Swagger Code Generator

## Overview

The Swagger Code Generator ([swagger-codegen](https://github.com/swagger-api/swagger-codegen)) is useful for generation of source code for client/server and documentation of APIs.

This sample code is to add an additional custom language or framework to the swagger codegen tool, without changing the original source code of swagger codegen tool.

## Build a custom language extension

This module adds the additional language `"nodejs-server-ex"` basend on the original language module `"nodejs-server"`.

In order to build this module, just execute `mvn package`.

~~~
$ mvn clean package
~~~

## How to use the custom language extension

In order to use this module, you can not use `-jar` option when executing the `swagger-codegen-cli.jar`, because java command ignores `-classpath` option and you can not add an additional classpath when you specify `-jar` option.

Instead, you must specify the main class of `swagger-codegen-cli` module along with the classpath of `swagger-codegen-cli.jar` and `swagger-codegen-nodejs-server-ex.jar`.

If you run the following command, you can see the additional available language name `"nodejs-server-ex"`:

~~~
$ java -classpath swagger-codegen-cli.jar:swagger-codegen-nodejs-server-ex.jar \
	io.swagger.codegen.SwaggerCodegen langs

Available languages: [ ..., nodejs-server-ex]
~~~

You can generate the custom source code based on this module as follows:

~~~
$ java -classpath swagger-codegen-cli.jar:swagger-codegen-nodejs-server-ex.jar \
	io.swagger.codegen.SwaggerCodegen generate \
	-i swagger.json \
	-l nodejs-server-ex \
	-o output-dir
~~~
