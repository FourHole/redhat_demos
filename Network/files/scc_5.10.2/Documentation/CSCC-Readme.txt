Distribution A: Approved for Public Release (16 Feb 2021) NIWCLANT SPR# 2021-50

Naval Information Warfare Center (NIWC) Atlantic

NAME
    CSCC - Command-Line SCAP Compliance Checker

SYNOPSIS
    cscc [options] [ file | path ]

	   
COMMAND LINE USAGE
       
The Security Content Automation Protocol (SCAP) Compliance Checker (SCC)
is a SCAP 1.3 Validated Scanner, with support for SCAP versions 1.0, 1.1
and 1.2, and an Open Vulnerability Assessment Language (OVAL) adopter, 
capable of performing compliance verification using SCAP content, and 
authenticated vulnerability scanning using OVAL content.
   
SCC has a separate executable for command line usage which is included
in the installation package as "cscc". CSCC allows for scripted or 
automated reviews by other applications or scheduled tasks.

Any  changes  made  via  the  Graphical  User Interface such as content
installation, or application preferences impact the command line inter-
face  and  vice  versa, as the options for both interfaces are saved to
the same "options.xml" file located in the SCC installation  directory.

################################################################################
CONFIGURATION PARAMETERS:

 Below are the parameters available for installing content and
 configuring application options. All of the following options must
 be used individually, and are not compatible with any other parameter.

 --config
   Open a command line menu which displays several configuration options

 -eb, --enableBenchmark BENCHMARK_ID [version]
   Enable a benchmark based on its ID, with optional benchmark version.
   Example:  ./cscc --enableBenchmark RHEL_8_STIG
   Example:  ./cscc --enableBenchmark RHEL_8_STIG 001.002
   See --listAllBenchmarks for a list of benchmarks.

 -db, --disableBenchmark BENCHMARK_ID [version]
   Disable a benchmark based on its ID, with optional benchmark version.
   Example:  ./cscc --disableBenchmark RHEL_8_STIG
   Example:  ./cscc --disableBenchmark RHEL_8_STIG 001.002
   See --listAllBenchmarks for a list of benchmarks.

 -ea, --enableAll
   Enable all SCAP and OVAL content.

 -da, --disableAll
   Disable all SCAP and OVAL content.

 -ub, --uninstallBenchmark BENCHMARK_ID [version]
   Uninstall a benchmark based on its ID, with optional benchmark version.
   Example:  ./cscc --uninstallBenchmark RHEL_8_STIG
   Example:  ./cscc --uninstallBenchmark RHEL_8_STIG 001.002
   See --listAllBenchmarks for a list of benchmarks.

 -ua, --uninstallAll
   Uninstall all SCAP and OVAL content.

 --setProfile PROFILE BENCHMARK_ID
   Set a profile to be applied to a specified content stream.
   See --listAllProfiles for a list of profiles.
   See --listAllBenchmarks for a list of benchmarks.
   Example: ./cscc --setProfile MAC-3_Sensitive RHEL_8_STIG

 --setProfileAll PROFILE
   Set a profile to be applied to all content installed in SCC, if
   applicable. If a profile cannot be applied to a content stream it is
   not applicable.  See --listAllProfiles to obtain a list of profiles.
   Example: ./cscc --setProfileAll MAC-3_Sensitive

 --setOpt OPTION VALUE
   Advanced user setting which allows command line configuration of any SCC
   option to a user specified value.
   --setOpt can be called multiple times in a single command if needed,
   see second example.
   Available options can be found in --listOpt, and need to be specified
   exactly. To set a value to an empty string, enter the value as all caps
   NULL
   Example: ./cscc --setOpt dirSessionEnabled 0
   Example: ./cscc --setOpt dirSessionEnabled 0 --setOpt debugEnabled 1

 --generateOptionsFile
   Delete the options file, restore default settings, and reinstall
   all content.  Note that this may take a few minutes.

 --generateAutoAnswerTemplates
   Delete and regenerarate all of the Manual Question auto-answer template files found in
   Resources/Content/Manual_Questions/Templates

 --restoreDefault
   Restore all options to installation default.

 -is FILE PROFILE [--force], --installScap FILE PROFILE [--force]
   Install one or more SCAP content streams from an XML file or ZIP archive.
   Specifying an XCCDF benchmark profile name after the filepath will enable
   that profile for the given SCAP stream. Use the optional --force switch to reinstall
   Example: ./cscc -is /home/user1/SampleScapContent.zip
   Example: ./cscc --installScap /home/user1/SampleScapContent.zip
   Example: ./cscc -is /home/user1/SampleScapContent.zip MAC-3_Sensitive
   Example: ./cscc -is --force /home/user1/SampleScapContent.zip
   Example: ./cscc --installScap --force /home/user1/SampleScapContent.zip MAC-3_Sensitive

 -isr FILE PROFILE [--force], --installScapRun FILE PROFILE [--force]
   Install, enable, and conduct an analysis with a SCAP Content
   stream from a zip file. Specifying an XCCDF benchmark profile name
   after the filepath will enable that profile for the given SCAP stream.
   Use the optional --force switch to reinstall.
   Example: ./cscc -isr /home/user1/SampleScapContent.zip
   Example: ./cscc --installScapRun /home/user1/SampleScapContent.zip MAC-3_Sensitive
   Example: ./cscc -isr --force /home/user1/SampleScapContent.zip
   Example: ./cscc --installScapRun --force /home/user1/SampleScapContent.zip MAC-3_Sensitive

 -iv FILE [--force], --installOval FILE [--force]
   Install OVAL Content from a single xml file or a zip file containing
   multiple xml files. Use the optional --force switch to reinstall.
   Example: ./cscc --installOval /home/user1/sampleOval.xml
   Example: ./cscc -iv --force /home/user1/sampleOval.xml

 -ivr FILE [--force], --installOvalRun FILE [--force]
   Install, enable, and conduct an analysis with OVAL Content from
   a single xml file or a zip file containing multiple xml files.
   Use the optional --force switch to reinstall.
   Example: ./cscc --installOvalRun /home/user1/sampleOval.xml
   Example: ./cscc -ivr --force /home/user1/sampleOval.xml

 --installTailoringProfile FILE
   Install an existing XCCDF Tailoring Profile file from another
   installation of SCC, created by the SCC GUI Tailoring interface.
   Installing a tailoring profile will set the selected profile for the matching content
   to be the tailored profile in the selected tailoring file
   Example: ./cscc --installTailoringProfile <filepath to tailoring xml>

 --checkForContentUpdates [--installUpdates | --installAll]
   Check for SCAP content updates from an online content repository.
   Additional settings may need to be pre-configured before usage.
   refer to: ./cscc --config -> Options -> Update Options
   Example: ./cscc --checkForContentUpdates
   Example: ./cscc --checkForContentUpdates --installUpdates
   Example: ./cscc --checkForContentUpdates --installAll

 --installUnixPlugin FILE
   Install the UNIX Plugin file, to allow SSH based scanning of remote UNIX hosts
   The file below can be obtained from the same location you downloaded SCC
   SCC_5.6.1_UNIX_Remote_Scanning_Plugin.scc
   Example:  ./cscc --installUnixPlugin /home/user1/SCC_5.6.1_UNIX_Remote_Scanning_Plugin.scc

   Refer to --installCredentialDB if this computer does not have the ability to open
   the SCC GUI to update/maintain the hosts/credentials

 --installCredentialDB FILE
   If this computer is not able to open the SCC GUI to create/maintain the SCC
   Host Credential Database, which is used to enter hosts and credentials for SSH
   based remote scanning of UNIX and Cisco devices, this feature allows you to install
   a previously created Host Credential Database and use it for scanning.
   *** NOTE 1:  You will not be able to create new hosts, or edit credentials, just perform
   scans using the Master Password for the existing set of hosts/credentials.  When
   host passwords expire, or the Master Password exires, you'll need to obtain an updated
   Host Credential DB and reinstall it via this command.
   *** NOTE 2:  This feature will always overwrite the existing host credential db (if found)
   You will need to manually copy the hostCredentials.db from another installation, by default
   it's found in <your home directory>/SCC/Config

 --register EMAIL REGISTRATION_CODE
   This command line argument is used to register your email address with a code
   provided from the SCC team, obtained by emailing scc.fct@navy.mil, indicating
   that your team/group/agency is planning to send some level of funding in the future.
   Registering your email address makes the funding notice go away.

 --upgrade FILE
   Upgrade the configuration options from a previous installation of SCC.
   SCC will load the current settings, and overlay the configuration settings from the selected
   option file, excluding content, appUpdateURL and contentRepository.
   Example: ./cscc --upgrade <filepath to existing SCC options xml>

################################################################################
SCANNING PARAMETERS:

 Below are the parameters available for performing scans. Many of the
 options can be used in combination, unless indicated below.

 Any configuration change from a Scanning Parameter is temporary, and does
 not get saved for future use.

 no parameters
   Review the local computer based on the configuration settings found
   in options.xml.  If options.xml does not exist in the installation
   directory, it will be created based on application defaults

 -d, --debug
   Create a verbose debug log file in the Logs directory for
   troubleshooting purposes.

 -ds, --debugToScreen
   Debug to the Screen.
   This option will print a very large amount of data to the terminal,
   which can be captured and shared with our team, and should only be
   used to help diagnose crash type issues.

 -ear, --enableAllRun
   Enable all SCAP and OVAL content and run content.

 -u DIRECTORY, --userDir DIRECTORY
   Temporarily configure SCC to save user results and logs to the specified
   directory path.
   Example: ./cscc -u /home/user1/

 -cd DIRECTORY, --configDir DIRECTORY
   Temporarily configure SCC to save application configuration files to the
   specified directory path.
   Example: ./cscc -cd /home/user1/

 --ssh [cisco|unix]
   Review all Cisco IOS/IOS-XE OR UNIX computers enabled in the Host
   Credential Manager, which is only available via the SCC GUI.
   You will be prompted to enter the SCC Host Credential Master Password in
   order to perform a remote command line SSH based scan.
   Note that many command line parameters such as -d, -q, -r, -mr, -ear
   are not compatible with --ssh and should be configured via --setOpt or
    --config prior to calling ./cscc --ssh
   '--ssh unix' can be used in combination with --wmi to scan both UNIX
   and Windows remotely at the same time.
   Refer to --installCredentialDB for installing an existing SCC Host Credential
   Database from another system which is able to use the SCC GUI

 --cisco FILE
   Conduct an offline review against a Cisco IOS/IOS XE configuration file or
   ZIP archive of multiple configuration files located at the given file path.

   **** Configuration files should be created with the 'show tech' command
   Example: ./cscc --cisco /home/user1/sampleConfigFile.txt

 -o FILE, --options FILE
   Review using the specified options file.
   Example: ./cscc -o options.xml
   Example: ./cscc --options /home/user1/myOptions.xml

 -q, --quiet
   Review in quiet mode. No output will be displayed on the screen.

 -r XCCDF_RULE_OR_OVAL_DEF, --rule XCCDF_RULE_OR_OVAL_DEF
   Review a single Rule using the Rule ID from the XCCDF file
   or review a single definition from an OVAL document.
   Example1: ./cscc -r account_lockout_duration
   Example2: ./cscc -r oval:mil.disa.stig.adobe.reader:def:1

 -mr RULE_COUNT RULE_ID RULE_ID .., --multipleRules RULE_COUNT RULE_ID...
   Review multiple rules using the Rule ID from the XCCDF file
   or review X definitions from an OVAL document.
   Example1: ./cscc -mr 2 account_lockout_duration logon_as_service 
   Example2: ./cscc --multipleRules 3 oval:mil.disa.stig.adobe.reader:def:1 oval:mil.disa.stig.adobe.reader:def:2 oval:mil.disa.stig.adobe.reader:def:3

 -rr XCCDF_RULE_ID_REGULAR_EXPRESSION --ruleRegex XCCDF_RULE_ID_REGULAR_EXPRESSION
   Review all rule IDs in the selected profile that match the regular expression
   Example1: ./cscc -rr rule_SV-213143r55.*
   Example2: ./cscc -ruleRegex mscp.content_rule_sysprefs_.*

################################################################################
POST SCAN REPORT GENERATION PARAMETERS:

 Below are the parameters available for creating reports after XML
 results have been created. All of the following options must be used
 individually, and are not compatible with any other parameter.

 -s OPTIONS_FILEPATH, --summaryReports OPTIONS_FILEPATH
   Generate SCAP summary reports using the specified options file.
   Example: ./cscc -s options.xml
   Example: ./cscc --summaryReports myOptions.xml

 -ts OPTIONS_FILEPATH, --detailedSCAP OPTIONS_FILEPATH
   Generate detailed reports for SCAP using the specified options file.
   Example: ./cscc -ts options.xml
   Example: ./cscc --detailedSCAP myOptions.xml

 -tv OPTIONS_FILEPATH, --detailedOVAL OPTIONS_FILEPATH
   Generate detailed reports for OVAL results using the specified options file.
   Example: ./cscc -tv options.xml
   Example: ./cscc --detailedOVAL options.xml

################################################################################
INFORMATIONAL PARAMETERS:

 Below are the parameters available for information purposes only.
 No configuration changes or scanning occur.  All of the following options must
 be used individually, and are not compatible with any other parameter.

 --checkForSCCUpdates
   Check to see if newer SCC releases exist via online query.
   Additional settings may need to be pre-configured before usage.
   refer to: ./cscc --config -> Options -> Update Options
   This does not download or update/install SCC, it just verifies it's current.

 --getOpt OPTION
   Advanced user setting to retrieve the value of any SCC option.
   Available options can be found with --listOpt, and need to be
   specified exactly.
   Example: ./cscc --getOpt debugEnabled
   debugEnabled = 0

 --listOpt
   Advanced user setting to retrieve the configurable values for use with
   --getOpt and --setOpt

 --listAllProfiles
   List all profiles according to the installed content. Note that not all 
   profiles are available to all content streams.

 --listAllBenchmarks
   List all benchmarks according to the content installed on the system. 
   Useful when setting a profile for specific content.

 -v, --version
   Display one liner version information.

 -V, --verboseVersion
   Display version information.

 -?, --help [config scan post-scan info]
   Display this help page, by default all sections will be displayed.
   With optional parameter(s) of config, scan, post-scan or info
   specific section(s) can be displayed.

EXAMPLES

Review localhost with customized report settings and do not display any 
data to the screen.

 # ./cscc -o myoptions.xml -q

Review localhost in debug mode and validate the XML files

 # ./cscc -d -x


SEE ALSO 
SCC_UserManual.pdf 

ONLINE RESOURCES 

SCC Page
https://www.niwcatlantic.navy.mil/scap/


