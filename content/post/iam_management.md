+++
title = "Authenticating Data for Experimentation Environment"
author = "Alejandro Armas"
tags = ["Programming", "Data Engineering"] 
date = 2023-10-30
+++


# Introduction    

In this post, I will explain how I streamlined team decision-making by building a cloud experimentation solution, secured by AWS IAM roles/policies, then optimized dataset network transmissions by **35x** 

In this post, we will explore how to leverage Terraform, a popular Infrastructure as Code (IaC) tool, to automate the setup and management of AWS IAM. We will walk through creating IAM roles, policies, and users, and demonstrating how to attach policies to these entities.

I prioritized building this tool, because a streamlined process was critical for Sachin and I to achieve consensus on datasets and features for a ML model. Exploratory Data Analysis is a process driven very different from software engineering. It involves lots of trial and error, so reproducibility was top of mind.

# Requirements

Recall the requirements in Part 1 of this blog post series.

| Requirements    | Motivation                                                                                                                                                                                     |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security        | I wanted measures that protected sensitive data with authentication and access control privileges                                                                                              |


# Design: Identity Access Management (IAM)


{{< figure src="/posts/reproducible_notebook/iam_user_interaction.png" alt="IAM User Interaction" caption="Figure 2: IAM User Interaction." class="figure-container">}}


## Usage for Users

There are two AWS accounts. One is for an admin. 


You have been assigned an IAM user account. It contains a basic permission to access the AWSCloudShell and assume a developer role. 

1. Go to the AWS Console and sign in as an [IAM user](https://us-east-2.signin.aws.amazon.com/oauth?client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&code_challenge=Df-eyHq1TuaY-VwR9zK7TvmArVTdcJ80SaE7Sp0e4LI&code_challenge_method=SHA-256&response_type=code&redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26nc2%3Dh_ct%26src%3Dheader-signin%26state%3DhashArgsFromTB_us-east-2_1d372fb131c13274&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEH0aCXVzLWVhc3QtMiJHMEUCIQDH7UZM4C3q4K7mPifQr6zEz6aSjsvmCzCp7C2xX7caBgIgTPkaVh03M0L4E9stTmn9BJiSexrZzDVa33Bhg%2B%2FaMQ4qigIIJxABGgw5MTQ1MzkxODcwMTMiDJhd7xseaZLYRzFKpCrnAXW8ANsEje0DBL2Q%2BTe4VPJyh5VwenkO2dtMAGt6q3d7uypvCvabAHspnBU2BkmEC%2F%2B8Hxnbt48cSU%2BVpMeYhXdorp4xvfWKSbeX3pXeoCUQ%2FlVMPI2Ees7F0%2BMKEu%2Bf%2Fv51qQwOhIiM1MRuS1yjLims1S2JmiwHsE2bxqSWznuImMpSGMkC0%2FbVWAdNvLklA1CC%2B1EiGpOTNYPoolqmZyELYqqps2UT6T1kIHb1Zn1Ri7fvTQoL%2Fy31CIxrK0OGAoaZ6ZKXIazy3pe6g1V9MTls6xIq6BMLlSCRZiAnOfHgxPBflHXLJTD3lrKmBjqPAZcpsdD5Y29r60sg37pPTDOFOpL0GIxq2w%2FhcUsEznpss%2Fd2MNmcypL7VuiJMBLxvcclncpKf%2BSi1QJUkydz7ICXGb4%2BacyHHWkf65JzlMPbXCU1zaaFYGsevszkeznwna0Tuub4QHPqLl1r76ijevjtInUfXdXy%2F0arB%2BG6cU9Rn%2BCrR6eZB4TL5oPWTPzk&X-Amz-Date=20230804T053324Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIA5J3WIRNCQGTQAM34%2F20230804%2Fus-east-2%2Fsignin%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=17d89954175e7e709f4f9ab21f01450b2de4656dc9b29775847c8fdb8b8ef23b)
2. Use the `account ID: 734281117891` associated with my administrator account
3. Sign in with your username: 
	- `sachin_loechler_god_data_scientist`
	- `nick_brown_certified_wizard`

{{< figure src="/posts/reproducible_notebook/aws_console_login.png" alt="Reproducible Notebooks">}}


After being issued a temporary password, the user then is prompted to choose their own password.

{{< figure src="/posts/reproducible_notebook/aws_console_change_password.png" alt="Reproducible Notebooks">}}


The user should now access the AWS console and see in themselves logged in, with the top right of the UI their `username` @ `account_id` 


{{< figure src="/posts/reproducible_notebook/aws_console.png" alt="Reproducible Notebooks">}}


##### Authorization Working as Intended

When a user first logs into their cloudshell instance, they are unable to list all the files in the object store `dvc-storage-tplzomcqordb`.

```bash
[cloudshell-user@ip-10-2-167-144 ~]$ aws sts get-caller-identity
{
    "UserId": "AIDA2V5UQWDB7O6M4LQD2",
    "Account": "734281117891",
    "Arn": "arn:aws:iam::734281117891:user/alejandro_demo_testing"
}
[cloudshell-user@ip-10-2-167-144 ~]$ aws s3 ls dvc-storage-tplzomcqordb
An error occurred (AccessDenied) when calling the ListObjectsV2 operation: Access Denied
```

##### Assuming New Role

Go to the AWSCloudConsole and enter: `aws sts assume-role --role-arn "arn:aws:iam::734281117891:role/freeway_monitoring_developer" --role-session-name you-can-type-literally-anything`

{{< figure src="/posts/reproducible_notebook/aws_cloud_shell.png" alt="Reproducible Notebooks">}}


Afterwards, you can copy the `AccessKeyId`, `SecretAccessKey`, and `SessionToken` keys. With that information you can now assume a new IAM role. Until then, the user is still not authorized to list the objects inside of the S3 bucket.


Once you are able to configure this identity, you will be authorized to access the files. 

```bash
[cloudshell-user@ip-10-2-167-144 ~]$ export AWS_ACCESS_KEY_ID=ASIA2V5UQWDB66AX7MFK
[cloudshell-user@ip-10-2-167-144 ~]$ export AWS_SECRET_ACCESS_KEY=18Mw4HNOTREALPILoWjysAqTd5hGzf+SG92t/3kT
[cloudshell-user@ip-10-2-167-144 ~]$ export AWS_SESSION_TOKEN=IQoJb3JpZ2luX2VjEH4aCXVzLWVhc3QtMSJGMEQCIE6MvVVxoVsRNz8o1wd7Zc3dglTm144ij0sX4gPE6FO5AiAweGMRZ0JTB0g2r99b97/DeyO1A6Xtg82pwHaH/zWxLCqsAggnEAAaDDczNDI4MTExNzg5MSIML8GREa7z8h2wK7zdKokCCDEI/Sim/RJCO5hx9biflV1TpIdLfXMKQ6/cZAlpw9Mtu51ArgOQ8/1R7c0pwOsQumoMM+2gabJriGLxHtbCCeZL52kJ63OjREaGz/+dKxXjE86guEzliKy8uVfgNFRCmllj/a2LD840L9mkbrbZ8lKNNiOxmJbV4GwMYAUpAjugHj0rbyNBvIat9I+BOqm0VldUfRpicH/ip5jag4/ksY2l8Vk99+5zYfyL4A735vw+t4yFc457jR60pl5FKJUqOmkXOJKeu8wb78iUYJ7uOxCGykRupYtPRiWSsD4sW0Ljp8idyT9LQmac9QASK1mwmCQcGYrDu+zlwzvTij5tf1ovt21U0KQ5NDC/pLKmBjqeAZzpYZix3jliFhdQAKCeGy4WjW/3wXFmcDJ1PhfDbuzRA/y3JaWt1IgqeE/V3VqtmASCCdwpbNm1LOJtp34CDTDYkUcTamumKuaGuqK/UyO+ns9LNC4BmGVp3KNhancInI6DBeWoE1ZoUIPnMJrxR9VJH0RrmRZohGznn1DnyiStuiHpbvpdrR/JUllmG8NmvUHFyma3WIo+L7lFqhLO

[cloudshell-user@ip-10-2-167-144 ~]$ aws s3 ls dvc-storage-tplzomcqordb
PRE files/
```


# Design

1. We have a policy `aws_iam_policy` for issued identities `aws_iam_user` for new-joiners.
2. The `aws_iam_policy` authorizes people to assume a new role `aws_iam_role`. This is for developers.
3. `aws_iam_role` gives them `aws_iam_policy_document`, which allows CRUD operations on the S3 object store. 

{{< figure src="/posts/reproducible_notebook/iam_internals.png" alt="Reproducible Notebooks">}}


#### Creating Default Accounts

Using Terraform code, I created multiple `aws_iam_user` resources and with the help of `aws_iam_user_policy_attachment`, I was able to attach a `aws_iam_policy`. 

```terraform
resource "aws_iam_user" "alejandro_demo_testing" {
  name = "alejandro_demo_testing"
}


resource "aws_iam_user_policy_attachment" "attach_alejandro_demo_testing_default_trust" {
  user       = aws_iam_user.alejandro_demo_testing.name
  policy_arn = aws_iam_policy.new_developer_trust_policy.arn
}
```

##### Choosing a Default Scope

It was a requirement for people to be able to join the team and have a basic role. Next, I wanted them to have a basic set of abilities. To me, it was easy to reason that as people stayed on the project, they would move into more senior roles. Those more specialized roles would give them authority that others might not have. 

#### Policy for New Teammates

When thinking about the authorization a new teammate might have, I thought it would make a lot of sense to let them access AWS CloudShell. I declared this inside of the `aws_iam_policy_document`. In addition to this, the policy allowed new teammates to assume another more 'senior' role as part of their onboarding. This was important, because I wanted users to feel ownership over their identity.

```terraform
data "aws_iam_policy_document" "new_developer_trust_policy_document" {
  statement {
    effect = "Allow"
    actions = [
      "sts:AssumeRole",
    ]
    resources = [
      aws_iam_role.developer.arn
     ]
    sid = "AllowAssumingRole"
  }
  statement {
    actions   = ["cloudshell:*"]
    resources = [
      "*"
    ]
    sid = "AWSCloudShellAccess"
  }
}

resource "aws_iam_policy" "new_developer_trust_policy" {
  name        = "trust_policy_for_new_developers"
  description = "This policy enables developers access to AWSCloudShell"
  policy = data.aws_iam_policy_document.new_developer_trust_policy_document.json
}
```

#### Sharing Default Password

Next, once an `aws_iam_user` identity was created for a new person, you'd be able to access its default password. This could be shared through a slack message.

```terraform
output "alejandro_demo_testing_password" {
  value     = aws_iam_user_login_profile.alejandro_demo_testing.password
  sensitive = true
}
```


#### Developer Account Policy

When the new person finished being onboarded, they would then be able to attain the priviledge of performing CRUD operations on the Object Store. This would give them access to the data and be ready to work on the project.

Here is how these actions are detailed:

```terraform
data "aws_iam_policy_document" "bucket_permissions_policy_document" {
  statement {
    effect = "Allow"
    actions = [
      "s3:PutObject",
      "s3:GetObject",
      "s3:DeleteObject",
    ]
    resources = [
      "${aws_s3_bucket.dvc_storage.arn}/*"
    ]
  }
  statement {
    effect = "Allow"
    actions = [
      "s3:ListBucket",
    ]
    resources = [
      aws_s3_bucket.dvc_storage.arn,
    ]
  }
}
```

The way one gets authority to perform these actions is through the Developer Role. Like I said, we can create `aws_iam_role` as a specialized role that new joiners are able to assume once they were done onboarding. It gives them `aws_iam_policy_document` for bucket persmissions. 

```terraform
resource "aws_iam_role" "developer" {
  name               = var.developer_name
  assume_role_policy = data.aws_iam_policy_document.assume_role.json
}

resource "aws_iam_role_policy" "team_developer_policy" {
  name   = "team_freeway_monitoring_developer_policy"
  role   = aws_iam_role.developer.id
  policy = data.aws_iam_policy_document.bucket_permissions_policy_document.json
}
```


# Conclusion

By leveraging AWS IAM roles and policies, we ensured that our cloud experimentation solution was both secure and compliant with best practices. This robust security framework not only protected sensitive data but also facilitated a streamlined decision-making process by enabling controlled access to critical resources. Ultimately, this contributed to the overall goal of enhancing reproducibility and efficiency in our Exploratory Data Analysis workflows.

