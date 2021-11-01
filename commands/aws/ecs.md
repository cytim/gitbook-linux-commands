# AWS: Elastic Container Service (ECS)

### Exec into the ECS Containers

> **Official News**  
> https://aws.amazon.com/blogs/containers/new-using-amazon-ecs-exec-access-your-containers-fargate-ec2/
>
> **Reference**  
> https://www.ernestchiang.com/en/posts/2021/using-amazon-ecs-exec/

1. Install the [Session Manager Plugin](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html) locally.

2. Attach the following policy to the task's role, so the task can use SSM to create a secure channel to run "exec".

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "ssmmessages:CreateControlChannel",
           "ssmmessages:CreateDataChannel",
           "ssmmessages:OpenControlChannel",
           "ssmmessages:OpenDataChannel"
         ],
         "Resource": "*"
       }
     ]
   }
   ```

3. Update the task definition to set `containerDefinitions[].linuxParameters.initProcessEnabled` to `true`.

   ```json
   {
     "containerDefinitions": [
       {
         "linuxParameters": {
           "initProcessEnabled": true
         }
       }
     ]
   }
   ```

4. Update the service to...

   1. use the latest task definition; and
   2. enable "execute command".

   ```sh
   aws ecs update-service \
     --cluster <ECS_CLUSTER_NAME> \
     --service <ECS_SERVICE_NAME> \
     --task-definition <TASK_DEFINITION_NAME> \
     --enable-execute-command \
     --force-new-deployment
   ```

5. Ensure "execute command" is ready.

   ```sh
    aws ecs describe-tasks \
      --cluster <ECS_CLUSTER_NAME> \
      --tasks <ECS_TASK_ID>

    # 1. Search for "enableExecuteCommand", the value should be `true`.
    # 2. Search for "ExecuteCommandAgent", the "lastStatus" should be `RUNNING`.
   ```

6. Exec into the container.

   ```sh
   aws ecs execute-command \
     --cluster <ECS_CLUSTER_NAME> \
     --task <ECS_TASK_ID> \
     --container <ECS_CONTAINER_NAME> \
     --interactive \
     --command "/bin/sh"
   ```
