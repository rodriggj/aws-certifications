# Configuration Management & Infrastructure as Code

## Cloud Formation 

### Topics 
1. **Templates**

2. **`YAML Files`**

3. **Parameters**
> A dynamic way to provide input to your AWS CF Template. Super helpful if you don't know the configuration **in advance.**. Also helpful if you want to `reuse` a template across the enterprise. **Caveat** - some inputs cannot be determined ahead of time. Use a parameter when the answer to this question is _Yes_. "Is the CF resource configuration likely to change in the future?"

> There are a suite of `psuedo-params` provided to you by AWS to reference common AWS components like AMIId, Region, etc.

4. **Resources**
> Resources are the only mandatory component of the CF template. They represent the various AWS Components that will be created and configured. Resources are **not dynamic** they must be **declaritively** invoked. Resources **can** reference one another via the `!Ref` function. 

5. **Mappings**
> `Mappings` are fixed variables witin your CF Template (hard coded). They are very useful when you are trying to differentiate between envs or accounts (e.g. Dev v Prod, Regions, AMI types, etc.)

> To instantiate mappings you call the function `FN::FindInMap`. The shorthand version of this is `!FindInMap [MapName, TopLevelKey, SecondLevelKey]`. Example `ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", 32]`. Here we reference a `psuedo-param` called `AWS::Region`.

6. **Outputs**
> The Outputs section declares _optional_ output values that we can import into other stacks. (You have to export them first). You can view outputs in AWS CLI. An example would be if you had a `Network CF Template`; you could use the outputs section to return the VPCId and SubnetIds, which could then be chained to another CF template. 

> Be aware if you have a CF stack that provides an output to another stack there is a dependency btwn these 2 stacks that will prohibit you from deleting either CF template. 

```yaml
Outputs:
    StackSSHSecurityGroup:
        Description: The SSH Security Group for our Company
        Value: !Ref MyCompanyWideSSHSecurityGroup
        Export: 
            Name: SSHSecurityGroup
```

7. **Cross-Stack Reference**
> In order to input the `Export`, you will need to create a `Cross-Stack Reference`. For this you need to use the `Fn::ImportValue` function. 

```yaml
Resources: 
    MySecureInstance: 
        Type: AWS::EC2::Instance
        Properties: 
            AvailabilityZone: us-east-1a
            ImageId: ami-a4c7edb2
            InstanceType: t2.micro
            SecurityGroups: 
               - !ImportValue SSHSecurityGroup
```

8. **Conditions**
> Conditions are used to control the creation of resources or outputs based on a condition. Common conditions are (e.g. Environment (dev/test/prod), AWS Region, _Parameter_ value). Each condition **can** reference another condition, parameter, or mapping. 

```yaml
Conditions: 
    CreateProdResources: !Equals [!Ref EnvType, Prod]
```

> The intrinsic values for conditions: `Fn::And, Fn::Equals, Fn::If, Fn::Not, Fn::Or`. Conditions can be applied to any resources / outputs / etc...

```yaml 
Resources: 
    MountPoint: 
        Type: "AWS::EC2::VolumeAttachment"
        Condition: CreateProdResources
```

9. **Intrinsic Functions**
> 




------

## Elastic Beanstalk

------

## Lambda 

------ 



### Resources 

Cloud Formation Resources 
- [ ] [AWS CloudFormation Resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)
