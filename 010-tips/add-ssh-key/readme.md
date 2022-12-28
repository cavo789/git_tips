# Add a SSH key

> [https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/GitHub-SSH-Key-Setup-Config-Ubuntu-Linux](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/GitHub-SSH-Key-Setup-Config-Ubuntu-Linux)

Stop to clone repositories using `https` and prefer the `git` protocol. 

Before being able to do this, you'll need to add a SSH key and here is how to proceed:

* Start a Linux console and jump to the `.ssh` folder: `cd ~/.ssh`,
* Now, create a key for your GitHub profile (identified by your email address): `ssh-keygen -o -t rsa -C "YOUR_EMAIL`,
* Press enter for each questions i.e. keep default values,
* When done, display the content of your key by running `cat id_rsa.pub` and keep that info on the screen temporarily. You'll need that info very soon.
* Surf to `https://github.com/settings/profile` and click on the `SSH and GPG keys` in the left sidebar,
* Click on the `New SSH key` button and give a title to your new key,
* Copy/paste your key in the `Key` field and, finally,
* Click on the `Add SSH key`.

From now, you'll be able to use `git clone` and the `git@` protocol.
