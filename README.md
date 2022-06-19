# copy-to-repo-action
Copies files from a workflow run to another repository

## Inputs

### `source_path`
**Required**
Source path in the workflow

### `target_repository`
**Required**
Target repository

### `target_branch`
The branch the source is copied to. If unset the default branch is used.

### `target_path`
**Required**
The path the source is copied to. Must contain the target file name.

### `commit_message`
**Required**
Commit Message

### `git_user_email`
The mail address used in the commit

### `git_user_name`
The mail address used in the commit

### `ssh_key`
**Required**
SSH key used for pushing and pulling.

## Outputs

*None*

## Usage

### Preparations

#### Create a new ssh-key

Run the following command:
```bash
ssh-keygen -f /tmp/deploy_key -N ''
```

#### Action Secret

Put the *private key* to the *Action secrets* of the source repository ( = the
repository that runs the action)
[Screenshot of Repository Settings -> Secrets -> Actions](https://user-images.githubusercontent.com/1056976/174482709-b97e1ff7-06f4-4346-a31c-71e115d26166.png)
![Screenshot of Repository Settings -> Secrets -> Actions -> New Secret](https://user-images.githubusercontent.com/1056976/174482811-ccbdf426-9cd2-47d9-a84b-d671c11b7faf.png)
* **Name**: An arbitrary identifier that will be used to identify the secret from within the pipeline
* **Value**: The content of `/tmp/deploy_key`.

#### Deployment Public Key

Put the *public key* to the *Deploy keys* of the target repository ( = the
repository where the files are copied to)
![Screenshot of Repository Settings -> Deploy Keys](https://user-images.githubusercontent.com/1056976/174483200-bd59e770-06ba-4076-87d7-8bed505b85cb.png)
![Screenshot of Repository Settings -> Deploy Keys -> Add New](https://user-images.githubusercontent.com/1056976/174484336-0aa1bf3f-deba-4dd0-896d-ffa28b9103c1.png)
* **Title**: An arbitrary identifier. It makes sense to mention the source repository here.
* **Key**: The content of `/tmp/deploy_key.pub`.
* **Allow write access**: Must be checked
