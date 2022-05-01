## Distro hopping checklist

Because it's difficult to remember these many things, so write it down and go one by one

- [ ] update and upgrade packages
- [ ] setup terminal
  - [ ] install zsh https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH#how-to-install-zsh-on-many-platforms
  - [ ] install zsh-syntax-highlighting https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md
  - [ ] install zsh-autosuggestions https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md
  - [ ] install omz https://github.com/ohmyzsh/ohmyzsh#basic-installation
  - [ ] install Fira code font https://www.nerdfonts.com/font-downloads
  - [ ] install starship https://starship.rs/guide/#%F0%9F%9A%80-installation
  - [ ] install fzf https://dev.to/budavariam/supercharge-your-command-line-2c9b
  - [ ] install fnm https://github.com/Schniz/fnm#using-a-script-macoslinux
    - [ ] copy to zshrc 
        ```
        export PATH=/home/sambit/.fnm:$PATH
        eval "`fnm env`"
        eval "$(fnm env --use-on-cd)"
        ```
    - [ ] add fnm completions
      - [ ] fnm completions --shell zsh
      - [ ] copy dump to `.oh-my-zsh/completions/_fnm`
  - [ ] install nodejs LTS `fnm install --lts`
  - [ ] install yarn v1 and pnpm
  - [ ] compare and update .zshrc with this https://github.com/soulsam480/dotfiles/blob/master/.zshrc
  - [ ] setup and add ssh keys for github https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
  - [ ] install docker and docker compose
    - [ ] https://docs.docker.com/engine/install/ubuntu/
    - [ ] run as non root https://docs.docker.com/engine/security/rootless/
    - [ ] docker-compose https://docs.docker.com/compose/install/
- [ ] install apps (prefer flatpak)
  - [ ] edge
    - [ ] login and start sync
  - [ ] vscode
    - [ ] login and start sync
    - [ ] install wakatime
      ```cfg
      [settings]
        exclude                    = """
            /home/zoro/projects/work/"""
      ```
  - [ ] telegram
  - [ ] OBS
  - [ ] zoom
  - [ ] VLC
  - [ ] proton VPN
  - [ ] flameshot
- [ ] Gnome extensions
    - [ ] user-theme@gnome-shell-extensions.gcampax.github.com
    - [ ] clipboard-indicator@tudmotu.com
    - [ ] Vitals@CoreCoding.com
    - [ ] sound-output-device-chooser@kgshank.net
    - [ ] ding@rastersoft.com
    - [ ] netspeed@alynx.one
- [ ] UI
  - [ ] install nordic darker theme
  - [ ] install gnome tweaks

### Some help when refreshing popos
- https://www.reddit.com/r/pop_os/comments/i7r1s3/missing_user/g16ktos/
- https://unix.stackexchange.com/questions/230166/mint-cant-login-your-home-directory-error

#### Steps after refresh install to restore user
- run `sudo ls -al /var/lib/AccountsService/users`
- logout and log in with old user
  - select not listed on login screen
  - enter username and password
- run `chsh -s /bin/bash old_username` to restore shell to bash
- run `sudo nano /var/lib/AccountsService/users/old_username`
  - change `systemAccount` to false
- log out and log in with old username and password
- restore home folder access
  - run 
  ```
  chown root:root /home
  chown -R username:username /home/username
  # where username is old username
  ```
  - logout and log in
- open settings > users > delete the new user (created during first boot after refresh install)
