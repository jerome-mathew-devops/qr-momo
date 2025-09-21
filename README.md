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

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
