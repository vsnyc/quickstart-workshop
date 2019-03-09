+++
title = "Create Scaffolding"
chapter = false
weight = 20
+++

The GitHub repository for each Quick Start includes the following folders:

- **ci** - (required) Contains the configuration file and parameter files used for automated testing.
- **templates** - (required) Contains the AWS CloudFormation templates for the Quick Start. All templates use the .template file extension.
- **scripts** - (optional) Contains the scripts and configuration files that are used in the Quick Start; for example, to orchestrate the bootstrap, install or configure an app, or update a host.
- **functions** - (optional) Contains lambda functions used in the Quick Start.
- **submodules** - (optional) Used for any referenced Quick Starts that are configured as submodules of the Quick Start. These follow the naming convention _/submodules/quickstart-repo-name_ where the contents are synced at a specific commit level.

Do not worry if some of the folders described above doesn't make sense, yet. As you follow along the rest of the workshop, things will get more clear.

### Copy repo URL

Copy the url of your github repo
![repo url](/images/copy-qs-workshop-path.png)

### Clone repo

Clone the repo by running the following command. Replace *GITHUB_REPO_URL* with your url.

`git clone GITHUB_REPO_URL`

You should see following output.
<pre>
$ git clone git@github.com:avattathil/qs-workshop.git
  Cloning into 'qs-workshop'...
  warning: You appear to have cloned an empty repository.
</pre>

### Create scaffolding
When a Quick Start repo is created by the Quick Start team, all the folders are pre-created for you. But, as you are creating your own repo for this workshop, you need to create necessary folders.

To make this task easy, we have pre-created the scaffolding and configurations files. Run the following commands to download the scaffolding and files.

1. Go to repo

 	`cd qs-workshop`

2. Download and load the content in your repo

	```
	curl https://raw.githubusercontent.com/aws-quickstart/quickstart-workshop-labs/master/workshop-base/base.tar | tar -x
	```

3. Add and Commit your changes

	`git add --all .`

	`git commit -a -m 'Load base content'`
	
	You should see the following output.
	
	<pre>
	[master (root-commit) ab0660b] Load base content
	 	 3 files changed, 33 insertions(+)
		 create mode 100644 ci/taskcat.yml
		 create mode 100644 ci/workshop_input.json
		 create mode 100644 templates/workshop.template.yaml
	</pre>

4. Now that you have your changes committed locally to your repo, we will push these changes to github remote master branch.

	`git push`
	
	You should see the following output.
	
	<pre>
	Enumerating objects: 7, done.
	Counting objects: 100% (7/7), done.
	Delta compression using up to 8 threads
	Compressing objects: 100% (6/6), done.
	Writing objects: 100% (7/7), 753 bytes | 753.00 KiB/s, done.
	Total 7 (delta 0), reused 0 (delta 0)
	To github.com:avattathil/qs-workshop.git
	** [new branch]      master -> master
	</pre>

### Create development branch

As a best practice, you should keep the development and release branches separate. We will use **develop** branch for development and **master** branch for releases of the Quick Start. Currently, we only have _master_ branch in our github repo. So, let's create a _develop_ branch from the _master_ branch.

1. Create a develop branch based on master

	`git checkout -b develop`

2. Push develop branch to remote and set the upstream

	`git push --set-upstream origin develop`
	
	Your  output should look like below:

	<pre>
	Warning: Permanently added the RSA host key for IP address '192.30.253.113' to the list of known hosts.
	Total 0 (delta 0), reused 0 (delta 0)
	remote:
	remote: Create a pull request for 'develop' on GitHub by visiting:
	remote:      https://github.com/avattathil/qs-workshop/pull/new/develop
	remote:
	To github.com:avattathil/qs-workshop.git
	** [new branch]      develop -> develop
	Branch 'develop' set up to track remote branch 'develop' from 'origin'.
	</pre>


