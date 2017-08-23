# Installing Blade CLI [](id=installing-blade-cli)

The installation procedure for Blade CLI depends on your operating system (e.g.,
Windows, MacOS, or Linux). Follow the installation instructions corresponding to
what you're using.

## Windows [](id=windows)

First install the Java Package Manager called jpm by using [this installer.](https://github.com/jpm4j/jpm4j.installers/blob/master/dist/jpm-setup.exe)

Once you've installed JPM, execute

    jpm install -f https://releases.liferay.com/tools/blade-cli/latest/blade.jar

Blade CLI is now installed on your Windows machine! To check that Blade CLI is
installed, run `blade` in your terminal window. If Blade CLI is installed
correctly, you'll see the Blade CLI options printed in your terminal.

If you have proxy requirements, see the
[Installing Blade CLI with Proxy Requirements](/develop/tutorials/-/knowledge_base/7-0/setting-blade-cli-proxy-requirments)
tutorial for more information.

## MacOS and Linux [](id=macos-and-linux)

For MacOS/Linux users, you can execute a shell script that downloads and
installs both JPM and Blade CLI.  To do this, execute

    curl https://raw.githubusercontent.com/liferay/liferay-blade-cli/master/installers/global | sudo sh

+$$$

**Note:** The previous curl command installs JPM globally. You can also install
JPM and Blade locally by running

    curl https://raw.githubusercontent.com/liferay/liferay-blade-cli/master/installers/local | sh

$$$

Blade CLI is now installed on your Mac/Linux machine! To check that Blade CLI is
installed, run `blade` in your terminal window. If Blade CLI is installed
correctly, you'll see the Blade CLI options printed in your terminal.

If you have proxy requirements, see the
[Installing Blade CLI with Proxy Requirements](/develop/tutorials/-/knowledge_base/7-0/setting-blade-cli-proxy-requirments)
tutorial for more information.

## Updating Your Blade CLI Installation [](id=verifying-your-blade-cli-installation)

If your Blade CLI version is outdated, you can run the following command to
automatically download and install the latest version of Blade CLI:

    blade update

For Windows users, the `blade update` command does not work because Windows
cannot update a file that is currently in use. To bypass this issue, you can use
JPM to update your version of Blade CLI:

    jpm install -f https://releases.liferay.com/tools/blade-cli/latest/blade.jar

Blade CLI is updated frequently, so it's recommended to update your Blade CLI
environment for new features. You can check your current installed version by
running `blade version`.

You've successfully learned how to install and update Blade CLI. Blade CLI
offers many
[`create` templates](/develop/reference/-/knowledge_base/7-0/project-templates)
to help build @product-ver@ applications. It also offers various ways to deploy
those apps and interact with your Liferay server. Be sure to explore more Blade
CLI tutorials to learn how.
