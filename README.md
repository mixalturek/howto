How to...?
==========

Various mini howto-s and code snippets based on daily work.


## Wiremock

    wiremock --port 10000
    
    echo '{ "targetBaseUrl": "https://circleci.com/" }' | http post http://localhost:10000/__admin/recordings/start
    echo '{ "targetBaseUrl": "https://circleci.com/", "captureHeaders" : { "Authorization" : { } } }' | http post http://localhost:10000/__admin/recordings/start
    
    http post http://localhost:10000/__admin/recordings/stop

    wiremock --port 10000 --proxy-all https://michal-experimental.atlassian.net/


http://localhost:10000/__admin/recorder/


## Verify a process is listening on a port

    nc -vz localhost 9092


## Tcpdump, pcap

    tcpdump -i lo0 tcp port 8080 or tcp port 8081 -w file.pcap


## Tcpdump, check that packets are flowing (no deadlock)

    tcpdump host aaa.successfactors.com or host bbb.scdemo.successfactors.com
    
    tcpdump host aaa.successfactors.com
    tcpdump host bbb.scdemo.successfactors.com


## Info about a DNS record

    dig ...
    whois ...


## OSX, shortcuts

- Show hidden files in open dialog
    - Cmd + Shift + .
- `Insert` key in Midnight Commander
    - Ctrl + T
    - https://apple.stackexchange.com/questions/169130/simulate-insert-key-in-mac-os-x


## OSX, unmount flash disk

    df
    diskutil unmount /Volumes/...


## Maven dependencies

    alias mvn_deps_update='mvn versions:use-latest-releases versions:update-parent versions:update-properties'
    alias mvn_deps_tree='mvn dependency:tree 2>&1 | tee deps.txt'
    
    mvn versions:display-dependency-updates
    mvn versions:display-plugin-updates
    mvn versions:display-property-updates

https://www.mojohaus.org/versions-maven-plugin/


## Java, set timezone externally

    -Duser.timezone=UTC


## slf4j logger

    private static final Logger LOGGER = LoggerFactory.getLogger(My.class);


## Logback, console

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration scan="true" scanPeriod="30 seconds">
        <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
            <target>System.err</target>
            <encoder>
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} %highlight(%-5level) %-45logger{45} [%-20thread]: %msg \(%file:%line\)%n%xThrowable{full}</pattern>
            </encoder>
        </appender>
    
        <root level="INFO">
            <appender-ref ref="CONSOLE"/>
        </root>
    </configuration>


## Switch to an different JDK

    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    export PATH=$JAVA_HOME/bin:$PATH
    
    alias javaHome8='export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 ; export PATH=$JAVA_HOME/bin:$PATH'
    alias javaHome11='export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ; export PATH=$JAVA_HOME/bin:$PATH'


## IntelliJ IDEA, disable formatting

    // @formatter:off
    ...
    // @formatter:on


## IntelliJ IDEA, disable rendering of doc comments

    Settings > Editor > Reader mode
    |x| Rendered documentation comments


## Reactor debug mode

    Hooks.onOperatorDebug();

https://projectreactor.io/docs/core/release/reference/#debug-activate


## Await in JUnit tests

    <dependency>
        <groupId>org.awaitility</groupId>
        <artifactId>awaitility</artifactId>
        <version>4.0.2</version>
        <scope>test</scope>
    </dependency>

	import static org.awaitility.Awaitility.await;
	
	await().atMost(1000, TimeUnit.MILLISECONDS).untilAsserted(() ->
                    assertThatThrownBy(() -> new Socket("127.0.0.1", configuration.getServerSocketPort()))
                            .isInstanceOf(ConnectException.class)
                            .hasMessageContaining("Connection refused"));


## Temporary directory in JUnit 5 test

    @Test
    void myTest(@TempDir Path tempDir) {
    
    }

https://www.baeldung.com/junit-5-temporary-directory


## Visible for testing annotation

    @com.google.common.annotations.VisibleForTesting
    

## JUnit, AssertJ exceptions

     assertThatThrownBy(() -> ...)
                .isInstanceOf(... .class)
                .hasMessageContaining("...");


## Jetbrains exposed, log SQL queries

    transaction {
        addLogger(StdOutSqlLogger)
        // Do stuff
    }
    
https://www.baeldung.com/kotlin-exposed-persistence#2-logging-statements


## Spring, activate a profile 

    --spring.profiles.active=local


## Spring, generate OpenAPI spec

```kotlin
    implementation("org.springdoc:springdoc-openapi-starter-webmvc-ui:2.8.5")
```

```kotlin
@Test
fun `should generate OpenAPI spec`() {
    val spec = mvc.perform(MockMvcRequestBuilders.get("/v3/api-docs.yaml"))
        .andExpect(status().isOk)
        .andReturn().response.contentAsString

    Files.writeString(Paths.get("/Users/.../openapi_generated.yaml"), spec)
}
```

https://www.baeldung.com/spring-rest-openapi-documentation


## Gradle, check latest dependencies

    ./gradlew dependencyUpdates

https://github.com/ben-manes/gradle-versions-plugin


## Gradle, update wrapper

    ./gradlew wrapper --gradle-version=5.3


## Gradle, list dependencies

    ./gradlew -q dependencies > deps.txt
    ./gradlew -q dependencies api:dependencies server:dependencies > deps.txt


## Gradle, refresh dependencies, skip cache

    ./gradlew clean build --refresh-dependencies


## Gradle, rerun tasks

./gradlew build --rerun-tasks


## The perfect Front-End Checklist

- https://frontendchecklist.io/
- https://github.com/thedaviddias/Front-End-Checklist


## CSS highlight images without alt attribute

    /* You forgot the `alt` attribute. */
    img[alt=""], img:not([alt]) { border: 5px dashed #c00; }


## Yarn, update dependencies

    yarn upgrade
    yarn upgrade-interactive --latest

https://eriksamuelsson.com/upgrade-all-dependency-versions-in-package-json-with-yarn/


## Yarn, switch among node versions

    nvm use system
    nvm use
    yarn


## HTML5 site templates 

https://html5up.net/


## Debian testing download

- https://cdimage.debian.org/cdimage/weekly-builds/amd64/iso-cd/
- https://www.debian.org/CD/http-ftp/
- https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/
- https://cdimage.debian.org/images/unofficial/non-free/images-including-firmware/weekly-live-builds/


## Debian, install local deb file with all dependencies

    dpkg -i package.deb
    apt-get install -y -f --fix-missing
    dpkg -i package.deb


## Debian, search a missing package

    apt-file search glk_huc_ver03_01_2893


## Git, empty commit

    git commit --allow-empty -m "Trigger build" && git push
    alias git_trigger_build='git pull && git commit --allow-empty -m "Trigger build" && git push'


## Python HTTP server

    alias pythonHttpServer='python3 -m http.server 50000'
    
https://blog.anvileight.com/posts/simple-python-http-server/


## Display brightness

    brightnessctl set 100%

    ls /sys/class/backlight/

    cat /sys/class/backlight/intel_backlight/brightness
    cat /sys/class/backlight/intel_backlight/max_brightness
    echo 19220 > /sys/class/backlight/intel_backlight/brightness    # ~ max
    echo 10000 > /sys/class/backlight/intel_backlight/brightness    # ~ common
    echo 4000 > /sys/class/backlight/intel_backlight/brightness     # ~ dark

    cat /sys/class/backlight/nv_backlight/brightness
    echo 100 > /sys/class/backlight/nv_backlight/brightness
    echo 80 > /sys/class/backlight/nv_backlight/brightness
    echo 60 > /sys/class/backlight/nv_backlight/brightness

https://wiki.archlinux.org/index.php/Backlight


## pkexec

	chmod 644 /home/mc/.Xauthority ; pkexec --user m env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY thunderbird ; chmod 600 /home/mc/.Xauthority
	chmod 644 /home/mc/.Xauthority ; pkexec --user m env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY google-chrome ; chmod 600 /home/mc/.Xauthority

https://askubuntu.com/a/332847


## Bind a socked on a reserved port without root permissions

    apt-get install authbind
    touch /etc/authbind/byport/443
    chmod 777 /etc/authbind/byport/443

    authbind --deep java -jar application.jar


## Httpie, print full request and response

	http --verbose POST ...
	
	# 'H' request headers 'B' request body 'h' response headers 'b' response body
	http --print HBhb POST ...


## ngrok

- Public URL and IP address for local development.
- HTTPS certificate signed by a trusted authority.

https://ngrok.com/


## RequestBin

- Public service to inspect incoming HTTP requests.
- https://github.com/Runscope/requestbin
- https://requestbin.io/
- http://requestbin.net/


## mocky

Mock REST server

https://www.mocky.io/


## ps, list full command line

    ps auxfww


## WebGoat

Learn the hack - Stop the attack

- https://webgoat.github.io/WebGoat/
- https://github.com/WebGoat/WebGoat
- https://owasp.org/www-project-webgoat/


## Burp proxy

- https://portswigger.net/burp
- https://portswigger.net/support/configuring-firefox-to-work-with-burp
- https://portswigger.net/support/installing-burp-suites-ca-certificate-in-firefox

In short...

- Download burp community edition.
- Use Firefox unless you already have burp setup some other way.
- Run Burp, then configure Firefox to use `localhost:8080` as a proxy, for all protocols.
- In Burp, Proxy->Intercept, Turn Intercept off, then open a HTTP link in firefox and verify you can see it in Proxy->HTTP history in Burp.
- In Firefox, open http://burp, Download CA certificate, then configure that as a Trusted Certificate Authority in Firefox Certificate Manager, select to Trust to identify websites. Burp should now be able to intercept HTTPS requests.


## Rust, project specific toolchain

    rustup override set nightly
    rustup override set nightly-2014-12-18
    rustup override set 1.0.0
    rustup override unset
    rustup show

https://rocket.rs/v0.4/guide/getting-started/#installing-rust


## Docker, interactively show resources and limits

    docker stats


## Docker, consumed disk space

    docker system df
    docker system df -v


## OSX, language in login screen

    sudo languagesetup

https://support.apple.com/en-us/HT202036


## OSX, screenshot

- Fullscreen: Command + Shift + 3
- Selection: Command + Shift + 4


## OSX, fix xcode command line tools

    sudo rm -rf /Library/Developer/CommandLineTools
    xcode-select --install

https://stackoverflow.com/questions/34617452/how-to-update-xcode-from-command-line
https://stackoverflow.com/questions/19907576/xcode-is-not-currently-available-from-the-software-update-server


## OSX, prevent the system from sleeping

    caffeinate
    caffeinate -t 3600

## OSX, unmount disk

    umount /dev/disk2s1
    diskutil unmount /dev/disk2s1


## Kafka, test leader re-balances

http://kafka.apache.org/documentation/#quickstart_multibroker

    bin/zookeeper-server-start.sh config/zookeeper.properties
    bin/kafka-server-start.sh config/server-1.properties
    bin/kafka-server-start.sh config/server-2.properties
    bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 2 --partitions 2 --topic my-replicated-topic
    
    bin/kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic my-replicated-topic
    bin/kafka-leader-election.sh --bootstrap-server localhost:9092 --election-type=preferred --all-topic-partitions
    
    # Stop and start one of the Kafka brokers and trigger elections.
    

## Webpage speed test

https://webpagetest.org/


## Generate HTTP load and plot the results in real-time

https://github.com/nakabonne/ali


## SaaS pricing

https://www.lennyrachitsky.com/p/saas-pricing-strategy


## Emailing for SaaS startups

https://sidemail.io/


## Icons

https://icon-icons.com/


## Bypass Chrome warning about expired certificates

Type `thisisunsafe` in the page.


## Resize all images

    sips -Z 1280 *.jpg

https://stackoverflow.com/questions/28489793/how-to-resize-images-using-terminal-on-mac-osx


# Ruby version manager

    brew install rbenv ruby-build
    rbenv install --list
    rbenv install --list-all
    rbenv install 3.2.0
    rbenv global 3.2.0
    rbenv init
    eval "$(rbenv init - bash)"
    gem install rails
    # gem env home
    bundle install
    rails g seed_migration add_more_teamspaces_premium_flag

https://superuser.com/a/340492


# HP m28w printer

- Connect the printer via USB
- HP smart
- Printer settings
- Advanced settings
- Networking
- Wireless configuration
  - refresh the list of networks
  - manually enter SSID
  - enable wpa2
  - just try to change something and save
  - or temporarily disable Smart connect in Wi-Fi router
  - ???


# Debugging jest tests in a browser

    screen.logTestingPlaygroundURL()

https://twitter.com/housecor/status/1770071018939281534?s=46&t=0Q_w6C2Ucqr5O9vgvqFnAg


# Postgres, collect input values into an array

    ARRAY_AGG(id)


# Postgres, list all schemas in DB

    select schema_name from information_schema.schemata order by schema_name;


# Unsure calculator

https://filiph.github.io/unsure/


# Software engineering laws

https://newsletter.manager.dev/p/the-13-software-engineering-laws
