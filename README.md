# David's Mac OS X 10.11 El Capitan Update Guide

Blatantly stealing the idea from Kevin Elliott's [El Capitan Guide](https://gist.github.com/kevinelliott/e12aa642a8388baf2499), I've decided to document as much as I can of my new computer setup guide. There's a lot to do when refreshing a computer or setting one up from scratch, but a bit of planning reduces a ton of pain later on. :relaxed:

If there are steps that you've noticed that I'm clearly missing, please let me know. If you want to fork this guide to make your own, go right ahead!



## Install Basic Software

This is the software that I use on a very regular basis. Not all software is listed, as this would be one of the most time consuming to keep up to date.

### Install from App Store
- [Airmail](https://itunes.apple.com/us/app/airmail-2.6/id918858936?mt=12)
- [Xcode](https://developer.apple.com/xcode/download/)
- [Keynote](https://itunes.apple.com/us/app/keynote/id409183694?mt=12)
- [Pages](https://itunes.apple.com/us/app/pages/id409201541?mt=12)
- [Noizio](https://itunes.apple.com/us/app/noizio/id928871589?mt=12)
- [Giphy Capture](https://itunes.apple.com/us/app/giphy-capture.-the-gif-maker/id668208984?mt=12)

### Install from the Web
- [Sublime Text 3](http://www.sublimetext.com/3)
- [NordVPN](https://nordvpn.com/profile/)
- [Aerial Screensaver](https://github.com/JohnCoates/Aerial/releases/download/v1.1/Aerial.zip)

### Homebrew
##### Run Xcode and accept the license

Homebrew can not install properly until this occurs.

##### Install Homebrew

```ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew doctor```

##### Install Homebrew extension Cask

```brew install caskroom/cask/brew-cask```

##### Install common applications via Homebrew

```brew install openssl
brew install wget
brew install lastpass-cli --with-pinentry --with-doc```

##### Install applications via Homebrew Cask

Seriously, barring the insertion of malicious code or lack of checksums (two things which should honestly scare me away of many), Cask is pretty useful. I'm choosing to be willfully ignorant, since broadcasting usage opens me up anyway, and this saves a lot of time.

``` 
brew cask install chrome
brew cask install firefox
brew cask install dropbox
brew cask install evernote
brew cask install rescuetime
brew cask install skype
brew cask install virtualbox
brew cask install vagrant
brew cask install slack
brew cask install flux
brew cask install iterm2
brew cask install owasp-zap
brew cask install sequel-pro
```


### Vagrant, VVV, VV

- Ensure that Virtual Box and Vagrant are installed
- Install vagrant-hostupdater `vagrant plugin install vagrant-hostsupdater`
- Install vagrant-triggers `vagrant plugin install vagrant-triggers`
- Clone VVV `git clone git://github.com/Varying-Vagrant-Vagrants/VVV.git vagrant-local`
- Move to vagrant-local `cd vagrant-local`
- Run our first Vagrant up and wait a long long time `vagrant up`
- Look, at this point you probably need a coffee or something. Relax, you're doing great, and treat yourself to that caffeinated goodness.
- Install Variable VVV ` brew install bradp/vv/vv`
- Setup [VV Blueprints](https://github.com/bradp/vv#blueprints)
- Install @topdown's VVV dashboard
```cd ~/vagrant-local/www/default
git clone https://github.com/topdown/VVV-Dashboard.git dashboard```
- Copy dashboard-custom.php to `vagrant-local/www/default/dashboard-custom.php`


### Set Up Applications

- Login to Chrome to download and setup extensions
- Setup all Airmail accounts and settings
- Login to Dropbox and get files
- Login to Evernote and enable Web Clipper
- Login to all active Slack teams


### Sublime Text 3
- License Sublime Text and SFTP (license and instructions in email)
- Sublime Text CLI `mkdir -p ~/bin && ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" ~/bin/subl`
- Install Package Control `import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)`
- Install Packages: Accessibility, ACF Snippets, BracketHighlighter, CSS Completions, Diffy, Genesis, Gist, JSLint, JSONLint, SFTP, Trailing Spaces, WordPress Developer Resources, WordPress Developer Assistant


### Gitting on with Git
- Xcode and git are installed, right?
- If so, running `xcode-select --install` will get you the prompts for the Xcode Command Line Tools
- Set some defaults up.
```git config --global user.name "David Laietta"
git config --global user.email "davidjlaietta@gmail.com"
git config --global github.user davidlaietta
git config --global color.ui true
git config --global push.default current
git config --global core.editor "subl -w"```
- Check that keychain helper is installed with `git credential-osxkeychain`
- If not installed, set that sucker up.
```curl -s -O http://github-media-downloads.s3.amazonaws.com/osx/git-credential-osxkeychain```
- Modify permissions on the helper so it can operate
`chmod u+x git-credential-osxkeychain`
- Move the helper so Git can access it. This command will ask you for your (computer user) password. As you're typing your password, it won't show the characters, press return when done typing it. `sudo mv git-credential-osxkeychain /usr/local/git/bin`
- Tells Git to use the helper `git config --global credential.helper osxkeychain`
- Check again to see if the helper is successfully installed `git credential-osxkeychain`
- Create a new SSH key for Github
```cd ~/.ssh
ssh-keygen -t rsa -b 8192 -C "davidjlaietta@gmail.com"```
- Confirm that ssh-agent is enabled `eval "$(ssh-agent -s)"`
- Add SSH key to ssh-agent `ssh-add ~/.ssh/id_rsa`
- Copy SSH key to clipboard `pbcopy < ~/.ssh/id_rsa.pub`
- Login to Github
- [Add SSH key to Github](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
- Confirm that you're good to go `ssh -T git@github.com`


### Alfred 2

I use [Alfred 2](https://www.alfredapp.com/) though not quite as in-depth as I could. Still, I've found a few workflows that have been useful time savers.

First thing is to enable the paid Powerpack. The license is in the email account that I purchased it with.

- [Route to contact or location]
(http://www.packal.org/workflow/route-contact-or-location) - type "route" and a name or address, get a Google Map from my current location
- Install Capture::Tiny to make the Lastpass CLI work `sudo cpan install Capture::Tiny`
- [Lastpass CLI Workflow](http://www.packal.org/workflow/lastpass-cli-workflow-alfred) - Quickly search Lastpass
- Set Lastpass email in Alfred settings with `lpsetemail davidjlaietta@gmail.com`
- [Transmit](http://www.packal.org/workflow/transmit) - search and open favorites in Transmit 4 using the keyword "default ftp"
- [Launch URL in 3 browsers](http://www.packal.org/workflow/launch-url-3-browsers) - use "test" and a URL to open that site in Firefox, Chrome, and Safari
- [Network Tools](http://www.packal.org/workflow/network-tools) - make stuff like pings and cache flush fast
- [Wi-Fi Restart](http://www.packal.org/workflow/wi-fi-restart) - I hate needing this, but my computer just doesn't like staying connected. What am I doing wrong, computer!
- [Giphy](http://www.packal.org/workflow/giphy) - Use the command "giphy" to find the perfect gif
- [gitignore](http://www.packal.org/workflow/gitignore-0) - Create common .gitignore file templates. Use `gitignore-update` on first run to download templates
- [PHP Doc Search](http://www.packal.org/workflow/php-doc-search) - use "phpdoc" to search php.net
- [Alfred Drive Workflow](http://www.packal.org/workflow/google-drive) - Search Google Drive with "d"


## System Settings 

These are things that are a bit specific to my setup, but I find that they end up making my general computing experience that much nicer.

- Turn off all stupid notifications and badges/banners/butchers of concentration
- Set Chrome as the default browser
- Set Recent items to none
- Make dock nice and tiny
- Set time format to 24-hour time
- Change display energy saver settings
- Set key repeat to fast and delay untilr epeat to short
- Turn off keyboard brightness when computer is unused
- Setup replacement texts (like yall) so it doesn't try autocorrecting my informalities
- Add Colemak input source
- Set trackpad click to light, tracking speed to rather fast, and silent clicking
- Turn off launchpad trackpad gesture
- Setup internet accounts (email, Twitter, Facebook)
- Show bluetooth in menu bar
- Show battery percentage in menu bar
- Show date and time but not day in menu bar
- Ensure that guest account is off, and main account profile is set



At this point, you're probably done with computers, the internet, everything. At the very least, when you regain consciousness, your computer will be mainly good to go!