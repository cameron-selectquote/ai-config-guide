# AWS CLI Steering

Purpose: Standardize AWS access via AWS CLI using user-provided access keys.

## Default Approach
- Use AWS CLI for AWS access.
- Authenticate only with access keys provided by the user.
- Troubleshooting stays focused on CLI connectivity unless the user requests otherwise.

## Getting Access Keys (Console)
1. Sign in to the AWS Console.
2. Open IAM and select the user.
3. Go to **Security credentials**.
4. Under **Access keys**, choose **Create access key**.
5. Copy the **Access key ID** and **Secret access key**.

## Set Credentials as Environment Variables
```bash
export AWS_ACCESS_KEY_ID="<access-key-id>"
export AWS_SECRET_ACCESS_KEY="<secret-access-key>"
export AWS_SESSION_TOKEN="<session-token>"  # only if provided
```

## Optional: Use Credentials File
- Default path: `~/.aws/credentials`
- Profile format:
```ini
[default]
aws_access_key_id = <access-key-id>
aws_secret_access_key = <secret-access-key>
aws_session_token = <session-token>  # optional
```

## If the User Shares a Credentials File
- The user may provide a credentials file; use it directly instead of requesting keys again.
- Do not copy secrets into logs or steering files.

## Connectivity Check (CLI)
- Verify identity:
```bash
aws sts get-caller-identity
```
- Check config:
```bash
aws configure list
```

## Troubleshooting (CLI Only)
- Confirm `aws --version` returns a valid version.
- Verify `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY` are set in the shell.
- If using a profile, set `AWS_PROFILE` or use `--profile`.
- If region errors occur, set `AWS_DEFAULT_REGION` or run `aws configure set region <region>`.
- Re-test with `aws sts get-caller-identity`.

## Reference Links
- AWS CLI: https://aws.amazon.com/cli/
- Install/Update AWS CLI: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
- Configure Credentials: https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html
- IAM Access Keys: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html
- STS GetCallerIdentity: https://docs.aws.amazon.com/cli/latest/reference/sts/get-caller-identity.html
