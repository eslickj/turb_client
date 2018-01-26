# turb_client
Python package and utility scripts for communicating with the Turbine Science Gateway Web API, consisting of five Web JSON RESTful interfaces for Application, Session, Job, Consumer, and Simulation. 

## Installation

The turbine python module comes with a handy setup script that should install 
everything you need to run turbine and FOQUS.  There are multiple options 
for installation.  Please select the option that matches your needs.  Please 
report any failures to Jim Leek leek2@llnl.gov

If you are installing for multiple users and have root privledges, use this command:

    % python setup.py install

To install for only the current user (no root):

    % python setup.py install --user


## Extras

The 'turbine_session_graphs' script utilizes the python rpy2 module, which requires 
R and the ggplot2 package.

1) install R (Mac OS, Windows, Linux)
    
    http://cran.cnr.berkeley.edu/

2) install ggplot2 
    % R
    > install.packages("ggplot2")

3) install rpy2 python module
    % easy_install rpy2

## Dependencies

If setup.py worked correctly, you do not need to worry about these dependencies, 
they have already been installed.  If it failed, follow the directions to 
installal manually.  You need root priledges for these procedures.

1) dateutil

    DEBIAN:
    % apt-get install python-dateutil
    SETUPTOOLS:
    % easy_install dateutil

2) ntlm

    DEBIAN:
    % apt-get install python-ntlm
    SETUPTOOLS:
    % easy_install ntlm


## Running turbine scripts

     1) Copy Template configuration file
    
        * Localhost deployment copy 'config.txt.in' to 'config.txt'
        * Gateway Configuration Template copy 'config_turbine.acceleratecarboncapture.txt.in' to 'config.txt'

     2) Section Authentication:  Add your credentials to Username/Password.

     [Authentication]
     username=test1
     password=qwerty

     3) Security Section:  Add or Remove the trusted certificate authorities.

     [Security]
     TrustedCertificateAuthorities=cacerts.txt 

     * To disable server certificate verification remove the 'Security' section
     -- NOTE: IIS 7.5 self-signed certificates will not pass verification because the X509v3 Basic Constraints CA 
        bit is not set to TRUE.

     * option 'TrustedCertificateAuthorities' is a file containing all the trusted CA certificates.  Included
     in this distribution is the CA for use with 'localhost'.
     -- NOTE: It's a good idea to change the relative path to the absolute file path.

     4) Web Resource Sections (example for local deployment):

     [Consumer]
     url=https://localhost:8080/Turbine/consumer/
     [Job]
     url=https://localhost:8080/Turbine/job/
     [Simulation]
     url=https://localhost:8080/Turbine/simulation/
     name=mea-uq-billet-1
     [Session]
     url=https://localhost:8080/Turbine/session/
     [Application]
     url=https://localhost:8080/Turbine/application/

     * Edit the 'url' option as necessary
     
     % turbine_session_list config.txt
     []
     
     3) Logging

     [Logging]
     fileConfig=logging.conf


## Integration Tests

     1) Copy 'integration_test.cfg.in' to 'integration_test.cfg' in the test directory

     % cd test/integration
     % cp integration_test.cfg.in integration_test.cfg

     2) Copy & Paste all the information from config.txt into 'integration_test.cfg'.
     This is essentially all the URL's and the Username/Password.

     3) Run WS Basic tests 
     % python suites/ws_test_suite.py

     4) Run WS Simulation Basic tests 
     % python suites/simulation_test_suite.py 

     5) Run Application tests 
     % python suites/acm_test_suite.py
     % python suites/aspenplus_test_suite.py
     % python suites/excel_test_suite.py 
     
## Development Practices

* Code development will be peformed in a forked copy of the repo. Commits will not be 
  made directly to the repo. Developers will submit a pull request that is then merged
  by another team member, if another team member is available.
* Each pull request should contain only related modifications to a feature or bug fix.  
* Sensitive information (secret keys, usernames etc) and configuration data 
  (e.g database host port) should not be checked in to the repo.
* A practice of rebasing with the main repo should be used rather that merge commmits.

## Authors

* Josh Boverhof
* See also the list of [contributors](https://github.com/CCSI-Toolset/turb_client/contributors) who participated in this project.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, 
see the [tags on this repository](https://github.com/CCSI-Toolset/turb_client/tags). 

## License & Copyright

See [LICENSE.md](LICENSE.md) file for details
