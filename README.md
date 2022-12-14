# hello-world-from-quarkus
Source code for a Hello, World ! Quarkus application


## GitPod integration

To open the workspace, simply click on the *Open in Gitpod* button, or use [this link](https://gitpod.io/#https://github.com/k8s-operator-workshop/hello-world-from-quarkus).

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/k8s-operator-workshop/hello-world-from-quarkus)

## Workshop steps

Here you will find the different steps to create the đ Hello, World! đ Quarkus application.

### Requirements

Thanks to GitPod no technical requirements are needed, just copy and past the [.gitpod.yml](./.gitpod.yml) file to your repository and open your repository in Gitpod.  
See the [official documentation](https://www.gitpod.io/docs/getting-started/) of Gitpod to know how to open a project in Gitpod.

### Steps to create the project

âšī¸ The complete source of the project can be found in the [hello-world-from-quarkus-solution](https://github.com/k8s-operator-workshop/hello-world-from-quarkus-solution) repository. âšī¸

### Init and update the project

  - run the following command:

`quarkus create app com.workshop.operator:hello-world-from-quarkus  --extension=resteasy-reactive`

```bash
$ quarkus create app com.workshop.operator:hello-world-from-quarkus  --extension=resteasy-reactive

Picked up JAVA_TOOL_OPTIONS:  -Xmx3489m
-----------
selected extensions: 
- io.quarkus:quarkus-resteasy-reactive


applying codestarts...
đ  java
đ¨  maven
đĻ  quarkus
đ  config-properties
đ§  dockerfiles
đ§  maven-wrapper
đ  resteasy-reactive-codestart

-----------
[SUCCESS] â  quarkus project has been successfully generated in:
--> /workspace/hello-world-from-quarkus-workshop/hello-world-from-quarkus
-----------
Navigate into this directory and get started: quarkus dev
```
  - copy all the code in the `/workspace/hello-world-from-quarkus-workshop/hello-world-from-quarkus` folder in the root of the workspace, **don't copy the README.md to not override the initial README.md**
  - in the explorer view of VScode the following tree structure was created:
```bash
.
âââ README.md
âââ mvnw
âââ mvnw.cmd
âââ pom.xml
âââ src
    âââ main
    â   âââ docker
    â   â   âââ Dockerfile.jvm
    â   â   âââ Dockerfile.legacy-jar
    â   â   âââ Dockerfile.native
    â   â   âââ Dockerfile.native-micro
    â   âââ java
    â   â   âââ com
    â   â       âââ workshop
    â   â           âââ operator
    â   â               âââ GreetingResource.java
    â   âââ resources
    â       âââ META-INF
    â       â   âââ resources
    â       â       âââ index.html
    â       âââ application.properties
    âââ test
        âââ java
            âââ com
                âââ workshop
                    âââ operator
                        âââ GreetingResourceIT.java
                        âââ GreetingResourceTest.java
```
  - test the generated application by launching the `quarkus dev` command:
```bash
Listening for transport dt_socket at address: 5005
2022-09-15 08:34:33,419 WARN  [io.net.res.dns.DnsServerAddressStreamProviders] (build-5) Can not find io.netty.resolver.dns.macos.MacOSDnsServerAddressStreamProvider in the classpath, fallback to system defaults. This may result in incorrect DNS resolutions on MacOS.
__  ____  __  _____   ___  __ ____  ______ 
 --/ __ \/ / / / _ | / _ \/ //_/ / / / __/ 
 -/ /_/ / /_/ / __ |/ , _/ ,< / /_/ /\ \   
--\___\_\____/_/ |_/_/|_/_/|_|\____/___/   
2022-09-15 08:34:33,771 INFO  [io.quarkus] (Quarkus Main Thread) hello-world-from-quarkus 1.0.0-SNAPSHOT on JVM (powered by Quarkus 2.12.2.Final) started in 0.921s. Listening on: http://localhost:8080

2022-09-15 08:34:33,773 INFO  [io.quarkus] (Quarkus Main Thread) Profile dev activated. Live Coding activated.
2022-09-15 08:34:33,773 INFO  [io.quarkus] (Quarkus Main Thread) Installed features: [cdi, resteasy-reactive, smallrye-context-propagation, vertx]

--
Tests paused
Press [r] to resume testing, [o] Toggle test output, [:] for the terminal, [h] for more options>
```
  - test the greeting end point: `curl http://<8080-gitpoduser-helloworld-gitpodadresse>`
```bash
$ curl https://8080-philipparts-helloworldf-3qdxnpakspl.ws-eu64.gitpod.io/
Hello from RESTEasy Reactive
```

> âšī¸ Note that you can use Maven to launch the Quarkus application with the following command: `mvn quarkus:dev` âšī¸

  - update the unit test class `GreetingResourceTest.java` in the `./test/java/com/workshop/operator` as following:
```java
@Test
public void testHelloEndpoint() {
    given()
      .when().get("/hello")
      .then()
          .statusCode(200)
          .body(is("đ  Hello, World ! đ"));
}
```
  - in the Quarkus terminal press `r` and show that the test failed:
```bash
2022-09-15 17:56:34,905 ERROR [io.qua.test] (Test runner thread) ==================== TEST REPORT #1 ====================
2022-09-15 17:56:34,905 ERROR [io.qua.test] (Test runner thread) Test GreetingResourceTest#testHelloEndpoint() failed 
: java.lang.AssertionError: 1 expectation failed.
Response body doesn't match expectation.
Expected: is "đ  Hello, World ! đ"
  Actual: Hello from RESTEasy Reactive

        at io.restassured.internal.ValidatableResponseImpl.body(ValidatableResponseImpl.groovy)
        at com.workshop.operator.GreetingResourceTest.testHelloEndpoint(GreetingResourceTest.java:18)


2022-09-15 17:56:34,910 ERROR [io.qua.test] (Test runner thread) >>>>>>>>>>>>>>>>>>>> Summary: <<<<<<<<<<<<<<<<<<<<
com.workshop.operator.GreetingResourceTest#testHelloEndpoint(GreetingResourceTest.java:18) GreetingResourceTest#testHelloEndpoint() 1 expectation failed.
Response body doesn't match expectation.
Expected: is "đ  Hello, World ! đ"
  Actual: Hello from RESTEasy Reactive

2022-09-15 17:56:34,911 ERROR [io.qua.test] (Test runner thread) >>>>>>>>>>>>>>>>>>>> 1 TEST FAILED <<<<<<<<<<<<<<<<<<<<


--
1 test failed (0 passing, 0 skipped), 1 test was run in 1287ms. Tests completed at 17:56:34.
Press [r] to re-run, [o] Toggle test output, [:] for the terminal, [h] for more options>
```
  - fix the `GreetingResource` class in `./main/java/com/workshop/operator/`:
```java
@GET
@Produces(MediaType.TEXT_PLAIN)
public String hello() {
    return "đ  Hello, World ! đ";
}
```
  - see that the test now is ok:
```bash
2022-09-15 17:58:15,459 INFO  [io.qua.test] (Test runner thread) All tests are now passing


--
All 1 test is passing (0 skipped), 1 test was run in 159ms. Tests completed at 17:58:16 due to changes to GreetingResource.class.
Press [r] to re-run, [o] Toggle test output, [:] for the terminal, [h] for more options>
```

### Release and tag the application
  - create the JAR: `mvn clean package`
  - create the docker image: `docker build -f src/main/docker/Dockerfile.jvm -t 56hkk1xk.gra7.container-registry.ovh.net/workshop/<username>/hello-world-from-quarkus-workshop:1.0.0 .`, for example `docker build -f src/main/docker/Dockerfile.jvm -t 56hkk1xk.gra7.container-registry.ovh.net/workshop/wilda/hello-world-from-quarkus-workshop:1.0.0 .`
  - connect the docker client to the Harbor registry: `docker login 56hkk1xk.gra7.container-registry.ovh.net`
  - push the image previously created: `docker push 56hkk1xk.gra7.container-registry.ovh.net/workshop/<username>/hello-world-from-quarkus-workshop:1.0.0`, for example `docker push 56hkk1xk.gra7.container-registry.ovh.net/workshop/wilda/hello-world-from-quarkus-workshop:1.0.0`
  - push all the code to the repository
  - create the release 1.0.0 in Github: see [official documentation](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
> Note that the GitHub release version must be the same that the previously created docker image created  

Congratulation your application is released and the image is pushed to the registry !
