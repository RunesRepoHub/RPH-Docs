# What is Docker?

![pic](../img/docker.png)

??? bug "Docker Overview"

    ## Docker overview

    Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

??? info "The Docker platform"

    ## The Docker platform

    Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allows you to run many containers simultaneously on a given host. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work, and be sure that everyone you share with gets the same container that works in the same way.

    Docker provides tooling and a platform to manage the lifecycle of your containers:

    * Develop your application and its supporting components using containers.
    * The container becomes the unit for distributing and testing your application.
    * When you’re ready, deploy your application into your production environment, as a container or an orchestrated service. This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

??? tip "What can I use Docker for?"

    ## What can I use Docker for?

    **Fast, consistent delivery of your applications**

    Docker streamlines the development lifecycle by allowing developers to work in standardized environments using local containers which provide your applications and services. Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

    Consider the following example scenario:

    * Your developers write code locally and share their work with their colleagues using Docker containers. 
    * They use Docker to push their applications into a test environment and execute automated and manual tests.
    * When developers find bugs, they can fix them in the development environment and redeploy them to the test environment for testing and validation.
    * When testing is complete, getting the fix to the customer is as simple as pushing the updated image to the production environment.

    **Responsive deployment and scaling**

    Docker’s container-based platform allows for highly portable workloads. Docker containers can run on a developer’s local laptop, on physical or virtual machines in a data center, on cloud providers, or in a mixture of environments.

    Docker’s portability and lightweight nature also make it easy to dynamically manage workloads, scaling up or tearing down applications and services as business needs dictate, in near real time.

    **Running more workloads on the same hardware**

    Docker is lightweight and fast. It provides a viable, cost-effective alternative to hypervisor-based virtual machines, so you can use more of your server capacity to achieve your business goals. Docker is perfect for high density environments and for small and medium deployments where you need to do more with fewer resources.