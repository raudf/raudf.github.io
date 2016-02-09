---
layout: post
title: Gitlab-CI (Secure) variables 
---

I have been using variables in Gitlab-CI quite extensively and really like the way it nicely fits in Gitlab.  
In this blog post, I will illustrate the 2 type of variables that you can use, why you would use it and how.  
The only requirement here is to have a Gitlab account and a repository.  
I will not cover the code nor the server side setup in details here since it is just an example.  
It is to be noted that you can have private repository and CI on Gitlab for free.  

## Getting started
To enable Gitlab-CI, you will need a `.gitlab-ci.yml` file which is similar in fuction to the popular `.travis.yml` file.  
It is good habit to [lint](https://gitlab.com/ci/lint) your file before you commit them.  

``` yaml
before_script:
  - curl -sSf https://static.rust-lang.org/rustup.sh -o rustup.sh
  - sh rustup.sh -y --disable-sudo
  
compile_test_ship:
  script:
    - rustc hello.rs
    - ./hello|grep -q -w "Hello World!"   
    -  $ curl -F $CI_BUILD_REF:hello $proto://$username:$password@$myserver:$portnumber/$url
  only:
    - master
```
To will not dive further on the `.gitlab-ci.yml`.  
A quick look at the [quick start](http://doc.gitlab.com/ce/ci/quick_start/README.html) guide will help you to get the big picture.  
I always keep a tab open with the full [documentation](http://doc.gitlab.com/ce/ci/), just in case.    

## The variables
The interesting part of the file is the curl command arguments `$CI_BUILD_REF:hello $proto://$username:$password@$myserver:$portnumber/$url`.  
Here we can see the two types if variables, the **predefined variables**:`CI_BUILD_REF` and the **user-defined variables**: `proto:`, `username`, `myserver`, `portnumber`, `url`.   
The former are all caps and revolve around git and Gitlab.  
They give you access to build and project metadata.  
The later can be defined in the yaml file, Gitlab documentation refer to them as **YAML-defined variables**.  
They can also be defined in the GUI via `project settings -> variables -> add variable`, Gitlab documentation refer to them as **Secure Variables**.  
You can overwrite variables, as you [expect](http://doc.gitlab.com/ce/ci/variables/README.html) the Secure Variables take precedence over YAML-defined variables, both of which take precedence over Predefined Variables.  

## Predefine variables
Having access to predefine variable is really handy to automatically name things, especially version number with `CI_BUILD_TAG`.  
In this example I use `CI_BUILD_REF` which contains the commit hash to name the binary on the server side.  
As with any **metadata**, it is useful to print these to understand what is going on when you debug.  

## YAML-defined variables
These are the **boring** piece of data/configuration you might need for your project to run.  
Your software use environment variable for configuration right ? If not, well it probably **[should](https://medium.com/@kelseyhightower/12-fractured-apps-1080c73d481c)**.  
The piece of data that are not boring like password and username have no place here.  
Pieces of information that you do not want shared with the world should not be here.  

## Secure Variables
Using secure variable for **sensible information** is the obvious use case.  
If your project suddenly becomes visible to the world, you avoid an emergency password change.  
In a similar note, if you get into the habit of separating concerns, you will/should not leak sensible data on your project.  
The less obvious, but very valid use of the variable is to let forks have their own settings.  
You can have identical code base, all the down to the CI, but have different setting across different version of the code.  
One side effect of the feature is the **granularity** of access to the data.   
When you need to give someone read/write access to you project, but not the details of your infrastructure beyond the CI.  
There is likely more use cases, these are just the 3 that I encountered.  

## Secure not so secure
Giving your secrets to Gitlab.com is a choice, a choice to trust their security team.  
Or you can run your own security team, I use [Sameer Naik's docker image](https://github.com/sameersbn/docker-gitlab) to run my own Gitlab instance.  
You can run your own Gitlab instance and decide not to use secure variable.  
I would argue that in the life span or your repo, you will regret such decision.  
It might not be as secure as Travis CI and their [encrypted variable](https://docs.travis-ci.com/user/environment-variables/#Encrypted-Variables).  
Then again Secure Variables are easier to use than travis CI's Encrypted Variables by far.  
It depends what tradeoff do you prefer to live with. 

## Conclusion
I will never again (mistakenly or not) write any sensible information in plain text for my CI needs.  
Gitlab allows to hide secrets from sight and enable better habit.  
How about your sensible information ?  


## Notes
An example of legal `.gitlab-ci.yml` that does not do what you expect.

``` yaml
before_script:
  - curl -sSf https://static.rust-lang.org/rustup.sh -o rustup.sh
  - sh rustup.sh -y --disable-sudo
  
stages:
  - build
  - test
  - deploy

compile_time:
  stage: build
  script:
    - rustc hello.rs
  only:
    - master

a_bit_of_testing:
  stage: test
  script:
    - ./hello|grep -q -w "Hello World!"
  only:
    - master

ship_it:
  stage: deploy
  script:
    -  $ curl -F $CI_BUILD_REF:hello $proto://$username:$password@$myserver:$portnumber/$url
  only:
    - master
```

The rust source file:
``` rust
fn main() {
    println!("Hello World!");
}

```

