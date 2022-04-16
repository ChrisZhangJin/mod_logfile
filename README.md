# mod_logfile
the version for encrypt sip trace in freeswitch.log

# How to enable SIP trace printing in freeswitch.log?
1. enable console level in mod_logfile configuration.

```
<configuration name="logfile.conf" description="File Logging">
  <settings>
   <!-- true to auto rotate on HUP, false to open/close -->
   <param name="rotate-on-hup" value="true"/>
  </settings>
  <profiles>
    <profile name="default">
      <settings>
        <!-- File to log to -->
        <param name="logfile" value="/usr/local/freeswitch/log/freeswitch.log"/>
        <!-- At this length in bytes rotate the log file (0 for never) -->
        <param name="rollover" value="524288000"/>
                <!-- Maximum number of log files to keep before wrapping -->
                <!-- If this parameter is enabled, the log filenames will not include a date stamp -->
                <param name="maximum-rotate" value="32"/>
        <!-- Prefix all log lines by the session's uuid  -->
        <param name="uuid" value="true" />
      </settings>
      <mappings>
        <!--
             name can be a file name, function name or 'all'
             value is one or more of debug,info,notice,warning,err,crit,alert,all
             Please see comments in console.conf.xml for more information
        -->
        <!-- the console level must be included here!! -->
        <map name="all" value="console,info,notice,warning,err,crit,alert"/>
      </mappings>
    </profile>
  </profiles>
</configuration>
```

2. enable sip trace feature in the file of sip_profile.
both of files conf/sip_profiles/external.xml and conf/sip_profiles/internal.xml 
```
<param name="sip-trace" value="true"/>
```

# How to compile it after modifying the source code?
run the command below
```
# compile 
make mod_logfile

# install
make mod_logfile-install
```

# what kind of content will be encrypted?
the content between "sip:" and "@" will be replaced by "*"

here is the example:
```
------------------------------------------------------------------------
   INVITE sip:**********@1.2.3.4:5060 SIP/2.0
   Max-Forwards: 70
   From: "8966434525" <sip:********@1.2.3.4:5060>;tag=XgBrrrDUc5a8r
   To: <sip:***********@1.2.3.4:5060>

```


