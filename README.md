  # Fully Automated App Preview Environment

## What is a Preview Environment you may ask:
- A Preview Environment is a temporary, isolated environmenet that gets created automatically whenever a collaborator opens or updates a pull request. Basically it is a mini version of your production environment that exist only for as long as a PR exis

### `Problems solved by the Preview Environments`
- Live feature testing before Merge, that is every PR run in its own isolated environment that QA, developers and other personels can access their application via a generated link and view the application on the go.
- No Collisions in testing environment, that is each PR gets a seperate namespace/environment, so changes don't interfere with each other.
- Bugs are caught before merging.
- Teams can easily decide to approve or menge based on working demo and not just code.
- Reduces usage of resources as the environment is deleted immedaitely the PR is closed.

WITH THE PREVIEW ENVIRONMENT SYSTEM, ALL YOU NEED TO DO IS OPEN OR UPDATE A PR AND WATCH AS YOUR APPLICATION COMES LIVE.



### `How does all this happen?`
- A pull request is created my a developer.
- Pull_request opened or updated event triggers Github actions workflow
- Docker authenticates with repository, Build docker image and pushes to your specified Image repository
- Kubenetes pulls this new image, deploys to an isolated namesapce and creates a service which provides you with an accesible application URL link.
- Upon closure of ths PR, the namespace is deleted and enviroment cleaned up


![Preview Environment 2](https://github.com/user-attachments/assets/14308512-55c5-4200-b6e9-f89380471eda)



## `Key Components`

- Self-Hosted Runner. A self hosted runner was used here as it provides:
    - Better control over my github work flow as compared to github's hosted runners
    - Provides eased access to resources on my server as these self hosted runners are installed on your servers
    - Access to other tools such as Docker, Kubernetes on your server is made easy
    - Maximised security as the is no 3rd party server such as the github hosted servers handling your workflow
-  DockerHub, Stores versioned images for each PR
-  Kubernetes Manifests files (Depolyment.yaml and service.yaml) with ____IMAGE____ placeholder
-  Kubeconfig to access kubectl on server

  
## `Accessing the Preview Environment`

. The preview of your application can be gotten from the command **kubectl port-forward svc/[service_name] [container_portnumber] -n preview-pr-[pr number]**

### `Cleanup`

. Upon merge or closing of the PR, The created namespace is deleted and code cleaned

### `Lessons learned`
- Discovered the benefits of using self hosted runners as compared to github hosted runners
- Better version for docker images as to prevent later application errors
- Use of sed replacements to inject pushed image into deployment manifest files
- Discovered how to make application testing faster and more cost effective as the entire system lives just life span of the pr

### `Future Improvements`

