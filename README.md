Play! framework sample application on OpenShift
=========================

Play! is a Java Web framework for web developers made by Web developers. It's a clean alternative to bloated enterprise Java stacks that focuses on developer productivity and targets RESTful architectures.

More information can be found on the official Piwik website at http://www.playframework.org/

This git repository helps you get up and running quickly with a Play! framework installation on OpenShift Express. 

Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

Create a jboss AS 7.0 application

	rhc-create-app -a playapp -t jbossas-7.0 -l $USERNAME

You can optionally add MySQL support to your application

	rhc-ctl-app -a cake -e add-mysql-5.1

Check the conf/application.conf file for several options to configure your data source.

Add this upstream playapp quickstart repo

	cd playapp
	rm -rf *
	git remote add upstream -m master git://github.com/opensas/playapp-openshift-quickstart.git
	git pull -s recursive -X theirs upstream master

Then push the repo upstream to OpenShift

	git push

That's it, you can now checkout your application at:

	http://playapp-$yourlogin.rhcloud.com

Whenever you want to deploy your app, follow these steps, from the app's root folder

    play war -o deployments/ROOT.war --exclude deployments
    git add deployments
    git commit -m "a new deploy"
    git push

Check [this article](https://github.com/opensas/play-demo/wiki/Step-12.5---deploy-to-openshift) for more information, and a detailed step by step guide.


