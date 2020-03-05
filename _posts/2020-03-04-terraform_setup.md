---
layout: post
title: Terraform tutorials - Set up with GCP
---

Something a little different here.  I’ve found that I often am setting up a lot of infrastructure to serve applications and models and usually my approach is a bit ad-hoc.  I have some templates for making [Flask](https://www.palletsprojects.com/p/flask/) applications, but spinning up VMs and serving these apps is an exercise in what might be generously referred to as engineering (less generously: frantically scouring my history for StackOverflow articles).

I had heard of Terraform as a great way to template-ize infrastructure setups, so I figured now’s as good a time as any to figure out how to use it.

At my group at MIT we use [Google Cloud](https://cloud.google.com/), mainly because we set it up as part of an old project.  But the point of using Terraform here is that it can interact with [a wide array of providers](https://www.terraform.io/docs/providers/index.html).  So, at least in theory, I should be able to adapt my work here to another provider if the need comes up.

So what I’m going to do is post my findings from working through some tutorials.  In my experience, a lot of tutorials suffer from a bad case of out-of-date-itis.  It’s an understandable, but very prevalent, condition.  So maybe these notes will help.  At least, until they suffer the same fate.

I’m working from [this tutorial getting started with Terraform for GCP](https://cloud.google.com/community/tutorials/getting-started-on-gcp-with-terraform).

You’ll need to install Terraform, which I found best done on Mac with `brew install terraform`

You’ll also need to sign up for GCP, which is definitely not something I’ll be able to cover here

In the section “Getting project credentials”, you’ll set up a service account.  You’ll also need to configure the permissions (Role) in the IAM panel.  That means adding your service account’s email to the users and adjusting the Role.  For the tutorial I set it to Compute Instance Admin.  

In order to avoid a warning, you’ll need to modify the following:
```// Configure the Google Cloud provider
provider "google" {
 credentials = "${file("CREDENTIALS_FILE.json")}"
 project     = "flask-app-211918"
 region      = "us-west1"
}
```

To: 
```// Configure the Google Cloud provider
provider "google" {
 credentials = file("CREDENTIALS_FILE.json")
 project     = "flask-app-211918"
 region      = "us-west1"
}
```

Everything else works up to trying to SSH into the instance you’re creating.  You’ll need to go into the instance on the console and add the SSH public key to its list of SSH keys. 

Once you’ve set up everything and you get to this line in the tutorial:

ssh \`terraform output ip\` 

If your key has a different username than your machine’s, you’ll need to adapt it:

ssh -i path/to/ssh/private/key [SSH KEY USERNAME]@\`terraform output ip\`

That should get you into the VM.

Once you’ve created the Flask application, you can test that it’s working by running the following:

```
python app.py &
curl http://0.0.0.0:5000
```

This will run the Flask application, but give you back the command prompt so you can run the curl command.  The result should be a success and you should see the “Hello Cloud” response.

The rest of the tutorial should work swimmingly.  

Hope this was helpful! Next time on this series, I’ll dive in the deep end and try and set up a model pipeline.  Wish me luck!