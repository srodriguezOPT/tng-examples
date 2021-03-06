## What does the test do?

1. login to the target machine through ssh using the username and password configured as in the config file
2. execute a command "ls -l /tmp"
3. log out

## Compilation and execution of TTCN-3 code

1. Compilation of TTCN-3 to C++ code: `ttcn3_compiler -t *.ttcn`
2. Makefile generation: `ttcn3_makefilegen -f -t deployment.tpd` 
3. Compilation in `./build` repository: `make` 
4. Execution in `./build` : `ttcn3_start ./DeploymentTest../SSHCLIENTasp_demo.cfg` 

## Configuration file  
```

[LOGGING]

FileMask := LOG_ALL |TTCN_PORTEVENT | TTCN_DEBUG | ERROR | TESTCASE | STATISTICS | MATCHING
ConsoleMask := LOG_ALL |TTCN_PORTEVENT | TTCN_DEBUG | ERROR | TESTCASE | STATISTICS  | MATCHING
LogFile := "log/%e.%h-%r.log"
LogEventTypes := Yes
LogSourceInfo := Yes


[MODULE_PARAMETERS]

SSHCLIENTasp_functions.sshDefaultRespTimeout := 3.0
SSHCLIENTasp_functions.login_waittime := 10.0 //time in second that the test will wait for the response of login from the target machine


SSHCLIENTasp_demo.clientCount := 1
SSHCLIENTasp_demo.loginCount := 1
SSHCLIENTasp_demo.opCount := 1

SSHCLIENTasp_demo.nodeIPAddr := "localhost" //change to target machine's ip address
SSHCLIENTasp_demo.usrname := "test" //change to username of the target machine
SSHCLIENTasp_demo.pwd := "test" //change to password

[EXTERNAL_COMMANDS]


[MAIN_CONTROLLER]
TCPPort := 5678
#NumHCs := 1
KillTimer := 30.0


[TESTPORT_PARAMETERS]
///////////////////////////
// SSH
*.SSH_PCO.debug := "yes" //"no" for less logs
*.SSH_PCO.statusOnSuccess := "no"
*.SSH_PCO.remote_host := "localhost" //change to target machine's ip address
*.SSH_PCO.remote_port := "22"
*.SSH_PCO.ip_version := "4"
*.SSH_PCO.EOL := "UNIX"
*.SSH_PCO.assignEOL := "yes"
*.SSH_PCO.supressEcho := "yes"
*.SSH_PCO.supressPrompt := "no"
*.SSH_PCO.pseudoPrompt := "no"
*.SSH_PCO.prompt1 := "test@tango-VirtualBox:~" //one of prompt1 or regex_propt1 need to be configured. To be configured regarding to the target machine
//*.SSH_PCO.regex_prompt1 := "*t[a-z]#(3,3)rb@Proc_m0_s1:~> "
*.SSH_PCO.readmode := "buffered"
*.SSH_PCO.detectServerDisconnected := "yes"

[EXECUTE]
SSHCLIENTasp_demo.control

```
