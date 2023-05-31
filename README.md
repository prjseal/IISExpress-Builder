# IISExpress-Builder

A PowerShell script that sets up custom domains with Self Signed SSL certificates for your .NET Core sites in IIS Express

It was adapted from [https://github.com/mattou07/iis-builder](https://github.com/mattou07/iis-builder) so most of the credit goes to him.

## What problems does this tool solve?

- When working with multi site setup in a .NET Core web project you need to have different domains to test the different sites out but you only have one address e.g. https://localhost:45678
- Working with custom domains in IIS Express websites is complicated and difficult to setup.
- A lot of people wouldn't know how to use custom domains with IIS Express sites
- Installing Self Signed SSL certificates is difficult to do
- Getting the thumbprint from an SSL certificate and assigning it to an IIS Express website domain is not easy
- It is time consuming to set this all up and steps might be missed or done incorrectly due to inconsistency

## What does this tool automate for you?

This tool automates the following steps for you:

1. Checks if you already have valid SSL certificate installed for the domains you want, and if not it creates them for you
2. Gets the thumbprints from the certificates to be used later
3. Adds the custom domains to the hosts file and points them to 127.0.0.1
4. Edits the applicationHost.config file in the .vs folder, adding the bindings for you
5. Configures IIS Express for you to use the SSL certificate for these URLs

## Assumptions

- You are using Visual Studio and IIS Express for developing your .NET Core website locally
- You are using a Windows machine and you have a folder called `C:\Program Files (x86)\IIS Express` with a file in it called `IisExpressAdminCmd.exe`

## How to use the tool?

1. Open Visual Studio and run your website in IIS Express. This ensures you have a `.vs` folder and an `applicationhost.config` file in its subdirectories.
Your site will be running with a localhost and port number address by default.

## Site A
![Site A Frontend Before](/images/site-a-frontend-before.png)

## Site B
![Site B Frontend Before](/images/site-b-frontend-before.png)

2. Download the files `iis-express-builder.ps1` and `iis-express.config.json` from this repository and place those files in the root of your web project. (where your Program.cs file lives).
![Web Root](/images/web-root.png)

3. Edit the `iis-express-config.json` file to update it with the custom domains you would like to use for this project.
!![config json file](/images/config-json.png)

4. Run the `iis-express-build.ps1` file in PowerShell

## Before
![run the powershell script](/images/command-prompt-before.png)

## After
![powershell script after](/images/command-prompt-finished.png)

5. In Visual Studio, rebuild your solution and run your site again.

6. Visit one of the custom domains in the browser e.g. [https://sitea.localtest.me](https://sitea.localtest.me) and see that it works

## Site A
![Site A Frontend After](/images/site-a-frontend-after.png)

## Site B
![Site B Frontend After](/images/site-b-frontend-after.png)

7. If you are using Umbraco you might need to add the Cultures and Hostnames to see the sites on the correct URLs

# Credits

Thanks to Matt Hart for creating [IIS Builder](https://github.com/mattou07/iis-builder) in the first place and agreeing for me to release this separately.

Thanks to my employers [ClerksWell](https://clerkswell.com/) for allowing me the time to work on this during work hours.
