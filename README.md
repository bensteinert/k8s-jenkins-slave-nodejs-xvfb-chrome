<img src="https://cloutainer.github.io/documentation/images/cloutainer.svg?v5" align="right">

# k8s-jenkins-slave-nodejs-xvfb-chrome

[![](https://codeclou.github.io/doc/badges/generated/docker-image-size-430.svg)](https://hub.docker.com/r/cloutainer/k8s-jenkins-slave-nodejs-xvfb-chrome/tags/) [![](https://codeclou.github.io/doc/badges/generated/docker-from-ubuntu-18.04.svg)](https://www.ubuntu.com/) [![](https://codeclou.github.io/doc/badges/generated/docker-run-as-non-root.svg)](https://docs.docker.com/engine/reference/builder/#/user)

Kubernetes Docker image providing Jenkins Slave JNLP with Node.JS, xvfb and Google Chrome.


-----
&nbsp;

### Preinstalled Tools

| tool | version |
|------|---------|
| yarn                 | 1.19.1 |
| node.js              | 10.16.3 |
| npm                  | 6.9.0 |
| google-chrome-stable | 77.0.3865.120 |
| kubernetes cli	     | apt-get |
| Xvfb                 | apt-get |
| git                  | apt-get |
| curl, wget           | apt-get |
| zip, bzip2           | apt-get |
| jq                   | apt-get |

-----
&nbsp;

### Usage

Use with [Kubernetes Jenkins Plugin](https://github.com/jenkinsci/kubernetes-plugin) like so:

```groovy
podTemplate(
  name: 'nodejs-xvfb-chrome-v32',
  label: 'k8s-jenkins-slave-nodejs-xvfb-chrome-v32',
  cloud: 'mycloud',
  nodeSelector: 'failure-domain.beta.kubernetes.io/zone=eu-west-1a',
  containers: [
    containerTemplate(
      name: 'jnlp',
      image: 'cloutainer/k8s-jenkins-slave-nodejs-xvfb-chrome:v32',
      privileged: false,
      command: '/opt/docker-entrypoint.sh',
      args: '',
      alwaysPullImage: false,
      workingDir: '/home/jenkins',
      resourceRequestCpu: '500m',
      resourceLimitCpu: '1',
      resourceRequestMemory: '3000Mi',
      resourceLimitMemory: '3000Mi'
    )
  ]
) {
  node('k8s-jenkins-slave-nodejs-xvfb-chrome-v32') {
    stage('build and test') {
      sh 'mvn -version'
      sh 'git clone https://github.com/clouless/angular-4-unit-test-dummy.git'
      dir('angular-4-unit-test-dummy') {
        sh 'yarn'
        sh 'yarn test'
      }
    }
  }
}
```


-----
&nbsp;

### License

[MIT](https://github.com/cloutainer/k8s-jenkins-slave-nodejs-xvfb-chrome/blob/master/LICENSE) © [Bernhard Grünewaldt](https://github.com/clouless)
