# UnityGitHubActions

## Setup

- run docker container `docker run -it gableroux/unity3d:2019.3.12f1`  
- checkout to unity directory `cd /opt/Unity/Editor/`
- create manual activation file `./Unity -quit -batchmode -nographics -logFile -createManualActivationFile` output: `Unity_v2019.3.12f1.alf`
- activate Unity via UI and get a licence file: `./Unity_v2019.x.ulf` (for more detail see video)
- after activation copy `./Unity_v2019.x.ulf` to docker in editor folder: `/opt/Unity/Editor/`
- create encrypted unity cert in docker `openssl aes-256-cbc -e -in ./Unity_v2019.x.ulf -out ./Unity_v2019.x.ulf.enc -k {{ sault }}`
- copy encrypted file from docker to project into `.github` folder `docker cp {{ container Name/id }}:/opt/Unity/Editor/Unity_v2019.x.ulf.enc {{ project_path }}/.github/`
- setup GitHub UNITY_LICENSE_DECRYPT_KEY at GitHub secrets
- for more details see source video and `https://github.com/rdcm/UnityGitHubActions/blob/main/.github/` folder content

# Know Issues

- if run OpenSSL outside docker, possible errors on decrypt stage due to OpenSSL version mismatch
- this github actions pipeline adapted for creation `*.unitypackage` file

# Links

- source video: https://www.youtube.com/watch?v=-txXtAfViEQ