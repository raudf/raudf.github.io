---
layout: post
title: GitLab, GitHub and Bitbucket - Adding an SSH key
---

I recently had to add my SSH to few services including GitLab, GitHub and Bitbucket.  
As I added (some) SSH keys, I received some email about them.  

# A good email
What, in my opinion, makes a good email?  
I have 3 (totaly arbitrary) criteria I found important in this case.  

# The key
Well, first off, I want to know what ssh key we are talking about.  
GitLab provides the name/title for the key, which is a good start but not enough.  
GitHub provides the name and fingerprint, which is better already, yet you have to use `ssh-keygen -lf` to verify.  
Finally Bitbucket provides a the name, the type `ssh-rsa`, the first 17 and last 22 character o fthe key, along with the name.  
All emails provided a link to go to the SSH cofiguration.  

# The unsubscribe button
I'm sure that you too have you fair share of email.  
It is usually of good manner to provide a way to avoid further email.  
GitLab had the touch of telling I could configuree it, yet not link.  
GitHub didn't even mentionned it.  
Bitbucket at last had a link to the relevant part of the settings.  
While it is possibly a bad idea to not have a notification, giving people the choice is more than welcome.  


# The email itself
If you use email for long enough, you will see some convention.  
Mailing list for example often prefix the subject to add some clarity and help people sorting their email.  
Another one convention is the sender field, where it make sense to have a sensible name.  
GitLab doesn't prefix the subject: `SSH key was added to your account`, but at least the sender field make sense with `GitLab <gitlab@mg.gitlab.com>`.  
GitHub prefix the subject like so `[GitHub] A new public key was added to your account` and simple sender field `GitHub <noreply@github.com>`.  
Bitbucket prefix the subject like so `[Bitbucket] SSH key added to kyzh`, but it looks like I sent my self an email with `kyzh <notifications-noreply@bitbucket.org>`.  

# Conclusion
Bitbucket is the most imformative and useful email.  
I just don't understand why using my name to send me an email, that's confusing.  
Finally, GitLab is the only where you can tangibly make a difference by contributing code to change its email.  
