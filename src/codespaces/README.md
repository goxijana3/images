# GitHub Codespaces (Default Linux Universal)

## Summary

*Use or extend the new Ubuntu-based default, large, multi-language universal container for GitHub Codespaces.*

| Metadata | Value |  
|----------|-------|
| *Categories* | Services, GitHub |
| *Image type* | Dockerfile |
| *Published image* | mcr.microsoft.com/devcontainers/universal:linux<br />mcr.microsoft.com/devcontainers/universal:focal |
| *Published image architecture(s)* | x86-64 |
| *Container host OS support* | Linux, macOS, Windows |
| *Container OS* | Ubuntu |
| *Languages, platforms* | Python, Node.js, JavaScript, TypeScript, C++, Java, C#, F#, .NET Core, PHP, Go, Ruby, Conda |

See **[history](history)** for information on the contents of published images.

## Description

While language specific development containers can be useful, in some cases you may want to use more than one in a project without having to set them all up. In other cases you may be looking to create a general "sandbox" container you intend to use with multiple projects or repositories. The large container image generated here (`mcr.microsoft.com/devcontainers/universal:linux`) includes a number of runtime versions for popular languages lke Python, Node, PHP, Java, Go, C++, Ruby, and .NET Core/C#.

If you use GitHub Codespaces, this is the "universal" image that is used by default if no custom Dockerfile or image is specified. If you like what you see but want to make a few additions or changes, you can use a custom Dockerfile to extend it and add whatever you need.

The container includes the `zsh` (and Oh My Zsh!) and `fish` shells that you can opt into using instead of the default `bash`. It also includes [nvm](https://github.com/nvm-sh/nvm), [rvm](https://rvm.io/), [rbenv](https://github.com/rbenv/rbenv), and [SDKMAN!](https://sdkman.io/) if you need to install a different version Node, Ruby, or Java tools than the container defaults. You can also set things up to access the container [via SSH](#accessing-the-container-using-ssh-scp-or-sshfs).

You can decide how often you want updates by referencing a [semantic version](https://semver.org/) of each image. However, **note that only the most recent image is pre-cached in Codespaces**. For example:

- `mcr.microsoft.com/devcontainers/universal:1-focal`
- `mcr.microsoft.com/devcontainers/universal:1.3-focal`
- `mcr.microsoft.com/devcontainers/universal:1.3.3-focal`

See [history](history) for information on the contents of each version and [here for a complete list of available tags](https://mcr.microsoft.com/v2/devcontainers/universal/tags/list).

## Accessing the container using SSH, SCP, or SSHFS

This container also includes a running SSH server that you can use to access the contents if needed. To use it:

1. Create a codespace in [GitHub Codespaces](https://github.com/features/codespaces) (this is the default image) or open this container in Remote - Containers.

2. If you created a codespace using a web browser in GitHub Codespaces, setup the [VS Code extension and connect to it from your local VS Code](https://docs.github.com/en/github/developing-online-with-codespaces/connecting-to-your-codespace-from-visual-studio-code).

3. When connected to the codespace, use a terminal in VS Code to set a password when connecting:

   ```bash
   sudo passwd $(whoami)
   ```

4. Press <kbd>F1</kbd> and select **Forward a Port...** and enter port `2222`.

5. You're all set! You can connect using SSH as follows:

   ```bash
   ssh -p 2222 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null codespace@localhost
   ```

   The `-o` arguments are not required, but will avoid errors about the "known host" signature changing when doing this from multiple codespaces.

6. Enter the password you set in step 3.

That's it! Use similar arguments to those in step 5 when executing `scp` or configuring SSHFS.

## Using Conda
This dev container and its associated image includes [the `conda` package manager](https://aka.ms/vscode-remote/conda/about). Additional packages installed using Conda will be downloaded from Anaconda or another repository if you configure one. To reconfigure Conda in this container to access an alternative repository, please see information on [configuring Conda channels here](https://aka.ms/vscode-remote/conda/channel-setup).

Access to the Anaconda repository is covered by the [Anaconda Terms of Service](https://aka.ms/vscode-remote/conda/terms), which may require some organizations to obtain a commercial license from Anaconda. **However**, when this dev container or its associated image is used with GitHub Codespaces or GitHub Actions, **all users are permitted** to use the Anaconda Repository through the service, including organizations normally required by Anaconda to obtain a paid license for commercial activities. Note that third-party packages may be licensed by their publishers in ways that impact your intellectual property, and are used at your own risk.

## Using this image

While the image itself works unmodified, you can also directly reference pre-built versions of `Dockerfile` by using the `image` property in `.devcontainer.json` or updating the `FROM` statement in your own  `Dockerfile` to:

`mcr.microsoft.com/devcontainers/universal:1-linux`

Alternatively, you can use the contents of the `Dockerfile` to fully customize your container's contents or to build it for a container host architecture not supported by the image.

## License

Copyright (c) Microsoft Corporation. All rights reserved.

Licensed under the MIT License. See [LICENSE](https://github.com/devcontainers/images/blob/main/LICENSE).
