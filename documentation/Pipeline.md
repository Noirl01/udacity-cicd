## Pipeline Process

- Github
- CircleCI
- AWS S3
- AWS Elastic Beanstalk

| Pipe-line                       | Processes                           |
| ------------------------------- | ----------------------------------- |
| Github Push                     |                                     |
| CircleCI Build Trigger          |                                     |
|                                 | Front-End Installs Dependencies     |
|                                 | Front-End Build Scripts             |
|                                 | Back-End Installs Dependencies      |
|                                 | Back-End Build Scripts              |
| CircleCI Awaits Manual Approval |                                     |
| On Approval                     |                                     |
|                                 | Front-End Build Scripts             |
|                                 | Back-End Installs Dependencies      |
|                                 | Back-End Build Scripts              |
| CircleCI Awaits Manual Approval |                                     |
| On Approval                     |                                     |
| CircleCI Deploy Trigger         |                                     |
|                                 | Front-End & Back-End Deploy Scripts |
| AWS Elastic Beanstalk           | Back-End Deploys                    |
| AWS S3                          | Front-End Deploys                   |
