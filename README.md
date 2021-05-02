# Blue/Green Deployment
## DevOps, AWS, Terraform, CI/CD, IaC
### AWS CodePipeline, AWS CodeBuild
![](https://github.com/nathanjonjon/aws-terraform-blue-green/blob/master/architecture.png)
CI/CD pipeline that consists four parts:
1. Source
    Listen to changes of given branch
2. Build
    docker build and docker push to ECR
3. Test
    Create a staging env and run the service
4. Deploy
    Create production env and start blue/green deployment


### Application Load Balancer, Target Group, Auto-scaling Group, Launch Template, Launch Configuration
- Bootstrap by configurating and maintaining these AWS cloud infrastructure (blue infra) manaully.
- Application Load Balancer listens to two target groups for blue/green infra, and use Terraform to launch and destroy auto-scaling group that attaches to each target group.
- Customize the settings of auto-scaling group, launch config in `.tf`

### Terrafrom
1. Create staging instance and run the service
2. Destroy staging instance upon approval
3. Create green infrastructure
4. Reroute traffic to green when all green targets are healthy
5. Import existing blue infra and destroy them
6. Create new blue infrastructure
7. Reroute traffic to new blue infra, and destroy green infra when all blue targets are healthy