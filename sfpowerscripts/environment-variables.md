# Environment Variables

sfpowerscripts can be configured by utilizing the following environment variables for additional options.

| ENVIRONMENT VARIABLE                 | PURPOSE                                                                                                                                                  | DEFAULT VALUE |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| SFPOWERSCRIPTS\_DEFAULT\_SHELL       | Configures the shell that need to be used to execute scripts such as pre/post scripts, fetching artifacts etc                                            | sh            |
| SFPOWERSCRIPTS\_DEPLOYMENT\_OPTION   | Toggle between selective/full deployment of components in a package during supported features such as validation. Supported values are selective or full | full          |
| SFPOWERSCRIPTS\_PROCESS\_MAX\_BUFFER | Increase the size of the buffer used to retrieve results when using wrappers around cli or scripts                                                       | 5 MB          |
| SFPOWERSCRIPTS\_NOCOLOR              | Disables colored logging                                                                                                                                 |               |
| DISABLE\_SFDMU\_CHECK                | Disables check for sfdmu                                                                                                                                 |               |
