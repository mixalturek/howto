howto
=====

Various mini howto-s and code snippets based on daily work.


## Wiremock

    wiremock --port 10000
    
    echo '{ "targetBaseUrl": "https://circleci.com/" }' | http post http://localhost:10000/__admin/recordings/start
    echo '{ "targetBaseUrl": "https://circleci.com/", "captureHeaders" : { "Authorization" : { } } }' | http post http://localhost:10000/__admin/recordings/start
    
    http post http://localhost:10000/__admin/recordings/stop


http://localhost:8080/__admin/recorder/


## Tcpdump to pcap

    tcpdump -i lo0 tcp port 8080 or tcp port 8081 -w file.pcap


## Tcpdump check that packets are flowing (no deadlock)

    tcpdump host aaa.successfactors.com or host bbb.scdemo.successfactors.com
    
    tcpdump host aaa.successfactors.com
    tcpdump host bbb.scdemo.successfactors.com


## OSX shortcuts

- Show hidden files in open dialog
    - Cmd + Shift + .
- `Insert` key in Midnight Commander
    - Ctrl + T
    - https://apple.stackexchange.com/questions/169130/simulate-insert-key-in-mac-os-x

## OSX unmount flash disk

    df
    diskutil unmount /Volumes/...


## Maven dependencies

    alias mvn_deps_update='mvn versions:use-latest-releases versions:update-parent versions:update-properties'
    alias mvn_deps_tree='mvn dependency:tree 2>&1 | tee deps.txt'
    
    mvn versions:display-dependency-updates
    mvn versions:display-plugin-updates
    mvn versions:display-property-updates

https://www.mojohaus.org/versions-maven-plugin/


## Java set timezone externally

    -Duser.timezone=UTC


## Visible for testing annotation

    @com.google.common.annotations.VisibleForTesting


## slf4j logger

    private static final Logger LOGGER = LoggerFactory.getLogger(My.class);


## Git empty commit

    git commit --allow-empty -m "Trigger build" && git push
    alias git_trigger_build='git pull && git commit --allow-empty -m "Trigger build" && git push'


## Reactor debug mode

    Hooks.onOperatorDebug();

https://projectreactor.io/docs/core/release/reference/#debug-activate


## Assertj exceptions

     assertThatThrownBy(() -> ...)
                .isInstanceOf(... .class)
                .hasMessageContaining("...");


## The perfect Front-End Checklist

- https://frontendchecklist.io/
- https://github.com/thedaviddias/Front-End-Checklist


## CSS highlight images without alt attribute

    /* You forgot the `alt` attribute. */
    img[alt=""], img:not([alt]) { border: 5px dashed #c00; }


## Debian testing download

- https://cdimage.debian.org/cdimage/weekly-builds/amd64/iso-cd/
- https://www.debian.org/CD/http-ftp/
- https://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/
- https://cdimage.debian.org/images/unofficial/non-free/images-including-firmware/weekly-live-builds/


## Debian install local deb file with all dependencies

    dpkg -i package.deb
    apt-get install -y -f --fix-missing
    dpkg -i package.deb


## Debian search a missing package

    apt-file search glk_huc_ver03_01_2893


## Python HTTP server

    alias pythonHttpServer='python3 -m http.server 50000'
    
https://blog.anvileight.com/posts/simple-python-http-server/


## Switch to an older JDK

    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    export PATH=$JAVA_HOME/bin:$PATH
    
    alias javaHome8='export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 ; export PATH=$JAVA_HOME/bin:$PATH'
    alias javaHome11='export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 ; export PATH=$JAVA_HOME/bin:$PATH'


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


## IntelliJ IDEA, disable formatting

    // @formatter:off
    ...
    // @formatter:on


## pkexec

	chmod 644 /home/mc/.Xauthority ; pkexec --user m env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY thunderbird ; chmod 600 /home/mc/.Xauthority
	chmod 644 /home/mc/.Xauthority ; pkexec --user m env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY google-chrome ; chmod 600 /home/mc/.Xauthority

https://askubuntu.com/a/332847


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


## Bind a socked on a reserved port without root permissions

    apt-get install authbind
    touch /etc/authbind/byport/443
    chmod 777 /etc/authbind/byport/443

    authbind --deep java -jar application.jar


## Public URL and IP address for local development

https://ngrok.com/


## Mock REST server

https://www.mocky.io/


## HTML5 site templates 

https://html5up.net/


## Httpie print full request and response

	http --verbose POST ...
	
	# 'H' request headers 'B' request body 'h' response headers 'b' response body
	http --print HBhb POST ...
