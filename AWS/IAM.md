# IAM

1. 在身份账户(ID:256454142732)中创建一个开发用户，IAM用户名为zhangsan
2. 在生产环境账户（ID: 458556760960）中创建一个跨账户角色：CA-TEST，并分配s3存储桶的完全访问权限
3. 在身份账户(ID:256454142732)中配置允许用户zhangsan切换到生产环境账户（ID: 458556760960 ）的CA-TEST角色。

```ascii
身份账户（Identity Account）                 生产环境账户
Account-AWS账户ID:256454142732 -切换账户-> Account-AWS账户 458556760960  --> S3
IAM用户：zhangsan                           角色：CA-TEST
密码&访问密钥
```

Policy

```json
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": "sts:AssumeRole",
        "Resource": "arn:aws:iam::458556760960:role/CA-TEST"
    }
}
```
