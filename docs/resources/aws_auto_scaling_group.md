---
title: About the aws_auto_scaling_group Resource
---

# aws\_auto\_scaling\_group

Use the `aws_auto_scaling_group` InSpec audit resource to test properties of a single AWS Auto Scaling group. 

<br>

## Syntax

    # Ensure that an auto scaling group exists and test some properties/tags
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      it { should exist }
      its('min_size') { should be 1}
      its('desired_capacity') { should be 2 }
      its('max_size') { should be 4}
      its('launch_configuration_name') { should eq 'MyLaunchConfiguration'}
      its('vpc_zone_identifier') { should include 'subnet-1234'}
      its('tags') { should include({'key': 'Application', 'value': 'TestApplication', 'resource_type': 'auto-scaling-group', 'resource_id': fixtures['auto_scaling_group_test_name'], 'propagate_at_launch': true}) }
    end  

    # You may also use hash syntax to pass the auto scaling group name
    describe aws_auto_scaling_group(name: 'MyAutoScalingGroup') do
      it { should exist }
    end

## Resource Parameters

### Name

This resource expects a single parameter, the Auto Scaling Group that uniquely identifies the auto scaling group

See also the [AWS documentation on Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html).

<br>

## Properties

### min\_size

An integer indicating the minimum number of instances in the auto scaling group
    
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      its('min_size') { should eq 1}
    end

### maximum\_size

An integer indicating the maximum number of instances in the auto scaling group
    
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      its('max_size') { should eq 5}
    end


### desired\_capacity

An integer indicating the desired  number of instances in the auto scaling group
    
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      its('desired_capacity') { should eq 3}
    end

### launch\_configuration\_name

The name of the auto scaling launch configuration associated with the auto scaling group
    
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      its('launch_configuration_name') { should eq 5}
    end

### vpc\_zone\_identifier

An array of strings corresponding to the subnet IDs associated with the auto scaling group
    
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      its('vpc_zone_identifier') { should include 'subnet-1234'}
    end

### tags

An array of objects with each object corresponding to a tag associated with the auto scaling group
    
    describe aws_auto_scaling_group('MyAutoScalingGroup') do
      its('tags') { should include({'key': 'Application', 'value': 'TestApplication', 'resource_type': 'auto-scaling-group', 'resource_id': fixtures['auto_scaling_group_test_name'], 'propagate_at_launch': true}) }
    end
<br>

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [matchers page](https://www.inspec.io/docs/reference/matchers/).

### exist

Indicates that the auto scaling group name provided was found.  Use `should_not` to test for auto scaling group names that should not exist.

    # Expect good news
    describe aws_auto_scaling_group('AnExistingASG') do
      it { should exist }
    end

    # No bad news allowed
    describe aws_auto_scaling_group('ANonExistentASG') do
      it { should_not exist }
    end

## AWS Permissions

Your [Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html#intro-structure-principal) will need the `autoscaling:Describe*` actions with Effect set to Allow.
You can find detailed documentation at [Actions, Resources, and Condition Keys for Amazon Auto Scaling Groups](https://docs.aws.amazon.com/autoscaling/ec2/userguide/control-access-using-iam.html).
