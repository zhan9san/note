# EC2

```yaml
---
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-00e87074e52e6c9f9
      InstanceType: t2.micro
      SubnetId: subnet-0c11ba632221f7263
      Tags:
        - Key:  PatchGroup
          Value: "test"
```
